---
layout: default
title: Home
---

<div class="photo">
  <img src="{{ site.baseurl }}/assets/photo.jpg" alt="Deepanshu Kartikey">
</div>

# Deepanshu Kartikey's Homepage

Performance Engineer at [Clickpost](https://clickpost.ai). I go deep into
systems and make them faster. When I'm not optimizing production, I'm hacking
on the Linux kernel and building tools for fun. I have a [blog](/blog/), and
I'm also on [GitHub](https://github.com/deepanshuclickpost) and
[LinkedIn](https://www.linkedin.com/in/deepanshu-kartikey-16024498/).
Here is my [about](/about/) page.

---

Recent blog posts:

<ul class="recent-posts">
  <li>
    <span class="post-date">Jul 2026</span>
    <span>» <a href="https://www.clickpost.ai/blog/hidden-latency-in-the-network-where-apm-stops-looking" target="_blank">Hidden Latency in the Network: Where APM Stops Looking (Part 2)</a></span>
  </li>
  <li>
    <span class="post-date">Jun 2026</span>
    <span>» <a href="https://www.clickpost.ai/blog/hidden-latency-in-python" target="_blank">Hidden Latency in Python: Where APM Stops Looking (Part 1)</a></span>
  </li>
  <li>
    <span class="post-date">Mar 2026</span>
    <span>» <a href="/blog/2026/03/29/how-i-fixed-a-real-linux-kernel-bug/">How I Fixed a Real Linux Kernel Bug as a First-Time Contributor</a></span>
  </li>
  <li>
    <span class="post-date">Mar 2026</span>
    <span>» <a href="https://www.clickpost.ai/blog/fixing-recursive-deadlock-in-opentelemetrys-python-sdk" target="_blank">Fixing a recursive deadlock in OpenTelemetry's Python SDK</a></span>
  </li>
</ul>

[Blog index](/blog/)

---

## Talks

**Syzbot to Mainline: How I Merged 21 Kernel Patches as a First-Time Contributor**
Open Source Summit India 2026 · The Linux Foundation

<a href="https://www.youtube.com/watch?v=46tO3ZzGvD4&t=31s" target="_blank">YouTube recording</a> &nbsp;&middot;&nbsp;
<a href="/assets/Syzbot_to_Mainline_OSS_India_2026__1_.pdf" target="_blank">Slides (PDF)</a>

---

## Open Source Contributions

**1. Linux Kernel** — patches merged across ext4, kernel/fork, ntfs3,
atm/lec, bpf, mm, net, ocfs2 and more. Reviewed by Theodore Ts'o, Andrew
Morton, Christian Brauner, and others.

<a href="/kernel-contributions/">See all kernel patches &rarr;</a>

**2. OpenTelemetry** — Fixed a recursive deadlock in the Python SDK under
concurrent tracing load. Diagnosed root cause, wrote reproducer, merged upstream.

<a href="https://github.com/open-telemetry/opentelemetry-python-contrib/pull/4302" target="_blank">PR #4302</a> &nbsp;&middot;&nbsp;
<a href="https://www.clickpost.ai/blog/fixing-recursive-deadlock-in-opentelemetrys-python-sdk" target="_blank">Blog post</a>

[All contributions &rarr;](/contributions/)

---

## Tools

**TrackLeak** — Memory leak detector for Python. Hooks malloc and PyMem_*,
zero instrumentation, works on live processes.

<a href="/trackleak/">Read more &rarr;</a> &nbsp;&middot;&nbsp;
<a href="https://github.com/deepanshuclickpost/TrackLeak" target="_blank">GitHub</a> &nbsp;&middot;&nbsp;
<a href="https://www.clickpost.ai/blog/hunting-python-memory-leaks-at-the-c-level" target="_blank">Blog post</a>

**eBPF Thread Profiler** — Thread-level profiler for Python & Java using
kernel-level syscall tracing. Zero code changes.

<a href="/ebpf-profiler/">Read more &rarr;</a> &nbsp;&middot;&nbsp;
<a href="https://github.com/clickpost-ai/thread_profiling" target="_blank">GitHub</a> &nbsp;&middot;&nbsp;
<a href="https://www.clickpost.ai/blog/scaled-servers-while-curtailing-our-cloud-costs-using-ebpf" target="_blank">Blog post</a>

[Tools page &rarr;](/tools/)
