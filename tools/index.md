---
layout: default
title: Tools
---

# Tools

Open source tools I've built for systems debugging and performance analysis.

---

## TrackLeak

A memory leak detector for Python applications. Hooks directly into `malloc`
and `PyMem_*`, zero instrumentation, works on live processes.

<a href="/trackleak/">Read more &rarr;</a> &nbsp;&middot;&nbsp;
<a href="https://github.com/deepanshuclickpost/TrackLeak" target="_blank">GitHub</a> &nbsp;&middot;&nbsp;
<a href="https://www.clickpost.ai/blog/hunting-python-memory-leaks-at-the-c-level" target="_blank">Blog post</a>

---

## eBPF Thread Profiler

A kernel-level thread profiler for Python and Java. Traces syscalls to track
request lifecycles, lock wait times, and I/O blocking. Zero code changes.

<a href="/ebpf-profiler/">Read more &rarr;</a> &nbsp;&middot;&nbsp;
<a href="https://github.com/clickpost-ai/thread_profiling" target="_blank">GitHub</a> &nbsp;&middot;&nbsp;
<a href="https://www.clickpost.ai/blog/scaled-servers-while-curtailing-our-cloud-costs-using-ebpf" target="_blank">Blog post</a>
