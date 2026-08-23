---
layout: default
title: Blog
---

# Blog

Writing about Linux kernel internals, performance engineering, eBPF,
and systems debugging.

---

<ul class="post-list">
  <li>
    <div class="post-date">Jul 2026</div>
    <div class="post-title"><a href="https://www.clickpost.ai/blog/hidden-latency-in-the-network-where-apm-stops-looking" target="_blank">Hidden Latency in the Network: Where APM Stops Looking (Part 2) ↗</a></div>
    <div class="post-desc">How we used eBPF to find a 60-second nginx stall caused by a stale AWS ALB IP, and thousands of 502s caused by a 2-second gunicorn keep-alive race condition — both invisible to OpenTelemetry.</div>
    <div class="post-tags">ebpf · tcp · networking · nginx · aws · performance</div>
  </li>
  <li>
    <div class="post-date">Jun 2026</div>
    <div class="post-title"><a href="https://www.clickpost.ai/blog/hidden-latency-in-python" target="_blank">Hidden Latency in Python: Where APM Stops Looking (Part 1) ↗</a></div>
    <div class="post-desc">How we used eBPF to find latency hiding in gunicorn's handoff queue (causing 11-second customer timeouts) and a 3-second gen-2 GC pause freezing sibling threads through the GIL — before the first OpenTelemetry span ever started.</div>
    <div class="post-tags">ebpf · python · gunicorn · gc · gil · performance</div>
  </li>
  <li>
    <div class="post-date">Mar 2026</div>
    <div class="post-title"><a href="/blog/2026/03/29/how-i-fixed-a-real-linux-kernel-bug/">How I Fixed a Real Linux Kernel Bug as a First-Time Contributor</a></div>
    <div class="post-desc">Fixing a KASAN use-after-free in atm/lec using RCU, with review from Eric Dumazet. What I learned about kernel development and the open source community.</div>
    <div class="post-tags">kernel · rcu · networking · syzbot · open-source</div>
  </li>
  <li>
    <div class="post-date">Mar 2026</div>
    <div class="post-title"><a href="https://www.clickpost.ai/blog/fixing-recursive-deadlock-in-opentelemetrys-python-sdk" target="_blank">Fixing a recursive deadlock in OpenTelemetry's Python SDK ↗</a></div>
    <div class="post-desc">Diagnosed and fixed a recursive deadlock in the OpenTelemetry Python SDK triggered under concurrent tracing load — merged upstream.</div>
    <div class="post-tags">opentelemetry · python · deadlock · concurrency · upstream</div>
  </li>
  <li>
    <div class="post-date">2025</div>
    <div class="post-title"><a href="https://www.clickpost.ai/blog/hunting-python-memory-leaks-at-the-c-level" target="_blank">Hunting Python memory leaks at the C level ↗</a></div>
    <div class="post-desc">How I built TrackLeak — hooking malloc and PyMem_* to find memory leaks in production Python apps with zero instrumentation.</div>
    <div class="post-tags">python · memory · c · trackleak · ebpf</div>
  </li>
  <li>
    <div class="post-date">2025</div>
    <div class="post-title"><a href="https://www.clickpost.ai/blog/scaled-servers-while-curtailing-our-cloud-costs-using-ebpf" target="_blank">Scaled servers while curtailing cloud costs using eBPF ↗</a></div>
    <div class="post-desc">Built an eBPF-powered thread profiler to trace syscalls at kernel level — tracking lock wait times and I/O blocking in Python and Java apps.</div>
    <div class="post-tags">ebpf · performance · python · java · kernel</div>
  </li>
</ul>
