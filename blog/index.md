---
layout: default
title: Blog
---

<p>
  Writing about Linux kernel internals, performance engineering, eBPF,
  and systems debugging. Some posts are hosted on the
  <a href="https://clickpost.ai/blog" target="_blank">Clickpost engineering blog</a>.
</p>

<h2>Posts</h2>

<ul class="post-list">

  <li>
    <div class="post-date">2025</div>
    <div class="post-title">
      <a href="https://www.clickpost.ai/blog/fixing-recursive-deadlock-in-opentelemetrys-python-sdk" target="_blank">
        Fixing a recursive deadlock in OpenTelemetry's Python SDK &rarr;
      </a>
    </div>
    <div class="post-desc">
      Diagnosed a recursive deadlock triggered under concurrent tracing load in
      OpenTelemetry's Python SDK. Traced the root cause through lock acquisition
      order, wrote a reproducer, and submitted a fix that was merged upstream.
    </div>
    <div class="post-tags">opentelemetry &middot; python &middot; deadlock &middot; concurrency &middot; upstream</div>
  </li>

  <li>
    <div class="post-date">2025</div>
    <div class="post-title">
      <a href="https://www.clickpost.ai/blog/scaled-servers-while-curtailing-our-cloud-costs-using-ebpf" target="_blank">
        Scaled servers while curtailing cloud costs using eBPF &rarr;
      </a>
    </div>
    <div class="post-desc">
      Built an eBPF-powered thread profiler that traces syscalls at the kernel level
      to track request lifecycles, measure lock wait times, and identify I/O blocking
      in Python and Java applications. Zero code changes. Used in production at Clickpost.
    </div>
    <div class="post-tags">ebpf &middot; performance &middot; python &middot; java &middot; syscalls &middot; production</div>
  </li>

</ul>

<p style="margin-top:24px;font-size:13px;color:#999;">
  More posts coming. Writing about kernel debugging, memory management, and eBPF internals.
</p>
