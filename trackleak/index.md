---
layout: default
title: TrackLeak
---

# TrackLeak

A memory leak detector for Python applications that hooks directly into the allocator.

---

## The Problem

Debugging memory leaks in production Python apps is painful. Traditional
profilers like `tracemalloc` add overhead and miss C-extension allocations
entirely. When your Python process is slowly eating memory in production,
you need something that works without restarting the process and without
adding instrumentation code.

## How It Works

TrackLeak intercepts both standard `malloc` and Python's `PyMem_*` functions
using `LD_PRELOAD`. It walks the Python stack to identify the source of each
allocation and tracks which allocations never get freed.

The result: a clear report showing exactly which functions are retaining
memory — with file paths, line numbers, and retention percentages.

## Features

<ul class="patch-list">
  <li><div><span class="patch-subsystem">zero instrumentation</span> no code changes needed in your application</div></li>
  <li><div><span class="patch-subsystem">live processes</span> works on already-running processes</div></li>
  <li><div><span class="patch-subsystem">C-extension aware</span> catches leaks that tracemalloc misses</div></li>
  <li><div><span class="patch-subsystem">minimal overhead</span> designed for production use</div></li>
  <li><div><span class="patch-subsystem">detailed output</span> file paths, line numbers, retention percentages</div></li>
</ul>

## Stack

<ul class="patch-list">
  <li><div><span class="patch-subsystem">language</span> C, Python</div></li>
  <li><div><span class="patch-subsystem">technique</span> LD_PRELOAD · malloc hook · PyMem_* interception</div></li>
</ul>

## Links

<ul class="patch-list">
  <li><div><span class="patch-subsystem">github</span> <a href="https://github.com/deepanshuclickpost/TrackLeak" target="_blank">github.com/deepanshuclickpost/TrackLeak</a></div></li>
  <li><div><span class="patch-subsystem">blog</span> <a href="https://www.clickpost.ai/blog/hunting-python-memory-leaks-at-the-c-level" target="_blank">Hunting Python memory leaks at the C level</a></div></li>
</ul>
