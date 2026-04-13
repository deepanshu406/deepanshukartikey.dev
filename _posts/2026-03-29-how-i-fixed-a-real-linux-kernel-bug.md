---
layout: post
title: "How I Fixed a Real Linux Kernel Bug as a First-Time Contributor"
date: 2026-03-29
tags: [kernel, rcu, networking, syzbot, open-source]
---

*What I Learned About RCU, Maintainers, and Open Source*

I am excited to share that I will be speaking at **Open Source Summit Mumbai 2026** on the topic "How I Merged 21 Patches as a First-Time Linux Kernel Contributor."

Before that talk, I want to share one of the most exciting and educational experiences of my journey — fixing a real Linux kernel use-after-free bug reported by syzbot, with guidance from some of the best kernel developers in the world.

This is not a story about being a genius. This is a story about good intentions, curiosity, and the incredible kindness of the Linux kernel community.

---

## What is Syzbot?

Syzbot is Google's automated kernel fuzzer. It runs 24/7, hammering the Linux kernel with random inputs to find bugs. When it finds one, it reports it publicly on syzkaller.appspot.com with a detailed crash report.

Anyone in the world can pick up one of these bugs and try to fix it. That is exactly what I did.

---

## The Bug

I picked up a syzbot bug report showing a KASAN use-after-free in `sock_def_readable()`. KASAN is the Kernel Address Sanitizer — when it says `slab-use-after-free`, it means some code is reading memory that has already been freed. This is a serious bug that can cause kernel crashes and security vulnerabilities.

The crash was happening in the ATM LAN Emulation subsystem in `net/atm/lec.c`. The call chain showed:

The original bug report that I fixed:
[syzbot report](https://syzkaller.appspot.com/bug?extid=f50072212ab792c86925)

```
mld_ifc_work -> lec_start_xmit -> send_to_lecd -> sock_def_readable -> CRASH
```

---

## Understanding the Race Condition

Using simple tools like `grep` and `sed`, I traced the bug to a classic race condition. Two functions were racing against each other:

`send_to_lecd()` uses the `lecd` pointer to communicate with the LEC daemon:

```c
if (!priv->lecd)       ->  check lecd, it is valid!
sk = sk_atm(priv->lecd) ->  use lecd
sk->sk_data_ready(sk)  ->  UAF CRASH HERE!
```

While `lec_atm_close()` clears it when the daemon disconnects:

```c
priv->lecd = NULL;     ->  socket freed via RCU!
```

The check and the use of `priv->lecd` were not protected. Another CPU could free the socket between the check and the use — classic use-after-free.

---

## Our First Attempt — v1 Patch

My initial approach was to use a spinlock + `sock_hold`/`sock_put` to protect the socket while it is being used. The idea was simple — hold a reference to the socket so it cannot be freed while we are using it.

I identified four vulnerable sites in `lec.c` and fixed all of them. I also added proper `skb` cleanup to prevent memory leaks on early exit paths.

I submitted this as v1 to the netdev mailing list. I was nervous — this was going to be reviewed by some of the best kernel developers in the world.

You can read the full v1 patch and Eric Dumazet's review here:
[v1 on lore.kernel.org](https://lore.kernel.org/all/20260309093614.502094-1-kartikey406@gmail.com/T/)

---

## The Review — Eric Dumazet

Within hours, I got a reply from Eric Dumazet, a top kernel networking developer at Google:

> "What prevents priv->lecd to be NULL after you released priv->lec_arp_lock? More generally, lec_atm_close() clears the sk_receive_queue. So allowing providers to queue more packets would be wrong. So really a better fix is needed."

Eric found two problems with my approach:

- I was still accessing `priv->lecd` directly after releasing the lock instead of using a local copy — the race window was still there.
- The spinlock did not prevent packets from being queued after `lec_atm_close()` drains the queue — timer and workqueue paths bypass `netif_stop_queue()`.

---

## Learning RCU

Eric hinted that an RCU-based approach would be better. I had heard of RCU before but never used it. So I had to learn it from scratch.

RCU stands for **Read Copy Update**. Think of it like a library book:

- Readers can read the book anytime, very fast, with almost no overhead.
- A writer who wants to replace the book must wait for ALL current readers to finish before removing the old book.

The three key rules of RCU:

- Writers use `rcu_assign_pointer()` to safely publish a new value.
- Readers use `rcu_read_lock()` and `rcu_dereference()` to safely access the value.
- `synchronize_rcu()` blocks until ALL readers across ALL subsystems have finished — guaranteeing no new packets can be queued after it returns.

---

## A Simpler Suggestion — Hillf Danton

Another developer, Hillf Danton, suggested a simpler approach — just reorder the calls in `lec_atm_close()` so `lecd` is cleared after stopping the queue and destroying the ARP table.

I investigated this seriously using code evidence. While `cancel_delayed_work_sync()` inside `lec_arp_destroy()` does stop `lec_arp_work`, the bug is triggered from `mld_ifc_work` — the IPv6 multicast workqueue which belongs to a completely different subsystem outside ATM/LEC control.

One simple command confirmed this:

```bash
grep -n "mld_ifc_stop" net/atm/lec.c  ->  empty output!
```

ATM/LEC has zero control over `mld_ifc_work`. After reviewing the evidence, Hillf agreed:

> "Syncing RCU after clearing lecd is the correct fix because lecd is checked with RCU lock held."

---

## The v2 Patch — RCU Based Fix

The complete fix involved converting `priv->lecd` to an RCU-protected pointer across all access sites:

- Mark `priv->lecd` as `__rcu` in `lec.h` to tell the kernel this pointer is RCU-protected.
- Use `rcu_assign_pointer()` in `lec_atm_close()` and `lecd_attach()` for safe pointer assignment.
- Use `rcu_read_lock`/`rcu_dereference`/`rcu_read_unlock` in `send_to_lecd()`, `lec_handle_bridge()` and `lec_atm_send()` to safely access `lecd`.
- Add `synchronize_rcu()` in `lec_atm_close()` after clearing `lecd` — guarantees all readers have finished before proceeding.
- Remove the redundant `sk_receive_queue` drain from `lec_atm_close()` since `vcc_destroy_socket()` already drains it afterwards.

Full v2 patch thread and discussion:
[v2 on lore.kernel.org](https://lore.kernel.org/all/20260309155908.508768-1-kartikey406@gmail.com/T/)

Merged commit:
[922814879542](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=922814879542c2e397b0e9641fd36b8202a8e555)

---

## What I Learned

### Technical Lessons

- Always read KASAN reports carefully — they tell you exactly what happened.
- Use simple tools: `grep`, `sed`, `git log` — they are enough to trace complex bugs.
- RCU is the right tool for protecting pointer lifetime in the kernel.
- Always back your arguments with code evidence — not assumptions.
- `synchronize_rcu()` is global — it waits for ALL readers across ALL subsystems.

### Community Lessons

- You do not need to be an expert to contribute — good intentions matter more.
- Maintainers are guides not gatekeepers — they want you to succeed.
- Review feedback is a gift not a rejection — every comment teaches you something.
- Always investigate suggestions seriously before accepting or rejecting them.
- The kernel community is one of the most welcoming technical communities in the world.

---

## My Message to You

When I started this journey, I did not know what RCU was. I did not know how syzbot worked. I did not know how to write a kernel patch.

But I had good intentions, a willingness to learn, and the courage to pick up a real kernel bug and see it through.

The Linux kernel community is one of the most welcoming technical communities in the world — if you approach it with respect and genuine desire to learn.

**You can do this too.**
