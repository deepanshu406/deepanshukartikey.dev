---
layout: default
title: eBPF Thread Profiler
---

# eBPF Thread Profiler

A kernel-level thread profiler for Python and Java applications using eBPF syscall tracing.

---

## The Problem

Debugging thread-level performance issues in production is hard. Traditional
profilers add overhead and often miss the real bottlenecks. When your servers
are slow under load and you don't know why — whether it's lock contention,
I/O blocking, or something else — you need visibility at the kernel level.

## How It Works

The profiler traces syscalls at the kernel level using eBPF. It tracks
request lifecycles, measures lock wait times, and identifies I/O blocking
for each thread — giving you X-ray vision into your application's threading
behavior. Zero code changes required. The eBPF program runs in the kernel
and attaches to your process from outside.

Built and deployed in production at Clickpost where it helped identify
performance bottlenecks and scale servers while reducing cloud costs.

## Features

<ul class="patch-list">
  <li><div><span class="patch-subsystem">zero code changes</span> attaches to running processes from outside</div></li>
  <li><div><span class="patch-subsystem">kernel-level tracing</span> syscall-level visibility, not sampling</div></li>
  <li><div><span class="patch-subsystem">lock wait time</span> measures exactly how long threads wait on locks</div></li>
  <li><div><span class="patch-subsystem">I/O blocking</span> identifies which I/O calls are blocking threads</div></li>
  <li><div><span class="patch-subsystem">minimal overhead</span> eBPF runs in the kernel, not in your app</div></li>
  <li><div><span class="patch-subsystem">Python & Java</span> works with both runtimes</div></li>
</ul>

## Stack

<ul class="patch-list">
  <li><div><span class="patch-subsystem">language</span> C, Python</div></li>
  <li><div><span class="patch-subsystem">technique</span> eBPF · bpftrace · BCC · syscall tracing</div></li>
</ul>

## Links

<ul class="patch-list">
  <li><div><span class="patch-subsystem">github</span> <a href="https://github.com/clickpost-ai/thread_profiling" target="_blank">github.com/clickpost-ai/thread_profiling</a></div></li>
  <li><div><span class="patch-subsystem">blog</span> <a href="https://www.clickpost.ai/blog/scaled-servers-while-curtailing-our-cloud-costs-using-ebpf" target="_blank">Scaled servers while curtailing cloud costs using eBPF</a></div></li>
</ul>
