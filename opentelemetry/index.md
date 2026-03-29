---
layout: default
title: OpenTelemetry Contributions
---

# OpenTelemetry Contributions

---

## opentelemetry-python-contrib

<ul class="patch-list">
  <li>
    <div>
      <span class="patch-subsystem">opentelemetry-python-contrib</span> —
      <a href="https://github.com/open-telemetry/opentelemetry-python-contrib/pull/4302" target="_blank">
        fix recursive deadlock in Python SDK
      </a>
      &nbsp;<span class="patch-hash"><a href="https://github.com/open-telemetry/opentelemetry-python-contrib/pull/4302" target="_blank">PR #4302</a></span>
    </div>
    <div class="patch-meta">Merged upstream into opentelemetry-python-contrib</div>
  </li>
</ul>

### What was the bug?

The OpenTelemetry Python SDK had a recursive deadlock triggered under
concurrent tracing load. When multiple threads attempted to initialize
tracing simultaneously, the SDK's internal lock was acquired recursively,
causing the process to hang indefinitely.

### How was it fixed?

Diagnosed the root cause by tracing lock acquisition order across threads.
Wrote a minimal reproducer to confirm the deadlock, then submitted a fix
that was reviewed and merged upstream into the official
opentelemetry-python-contrib repository.

<ul class="patch-list">
  <li>
    <div><span class="patch-subsystem">PR</span>
      <a href="https://github.com/open-telemetry/opentelemetry-python-contrib/pull/4302" target="_blank">
        github.com/open-telemetry/opentelemetry-python-contrib/pull/4302
      </a>
    </div>
  </li>
  <li>
    <div><span class="patch-subsystem">blog</span>
      <a href="https://www.clickpost.ai/blog/fixing-recursive-deadlock-in-opentelemetrys-python-sdk" target="_blank">
        Fixing a recursive deadlock in OpenTelemetry's Python SDK
      </a>
    </div>
  </li>
</ul>
