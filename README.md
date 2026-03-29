# deepanshukartikey.dev

Personal site — Linux kernel contributor, performance engineer.

## Structure

```
├── index.md           # Homepage
├── kernel/index.md    # All kernel patches with LKML links
├── blog/index.md      # Blog posts
├── tools/index.md     # TrackLeak, eBPF Profiler
├── about/index.md     # About page
├── _layouts/          # Page templates
├── assets/css/        # Stylesheet
└── _config.yml        # Jekyll config
```

## Run locally

```bash
bundle install
bundle exec jekyll serve
# open http://localhost:4000
```

## Deploy to GitHub Pages

```bash
# 1. Create repo named: deepanshukartikey.github.io
#    OR any repo + enable Pages in settings

git init
git add .
git commit -m "initial site"
git remote add origin https://github.com/deepanshuclickpost/deepanshukartikey.dev.git
git push -u origin main
```

Then in GitHub repo → Settings → Pages → Source: main branch → Save.

## Connect deepanshukartikey.dev domain

1. Buy domain on Namecheap
2. In Namecheap DNS settings add:
   - A record: @ → 185.199.108.153
   - A record: @ → 185.199.109.153
   - A record: @ → 185.199.110.153
   - A record: @ → 185.199.111.153
   - CNAME: www → deepanshuclickpost.github.io
3. In GitHub Pages settings → Custom domain → deepanshukartikey.dev
4. Check "Enforce HTTPS"

## Adding a new blog post

Create a file: `_posts/YYYY-MM-DD-title.md`

```markdown
---
layout: post
title: "Your Post Title"
date: 2025-04-01
tags: [kernel, ebpf, performance]
---

Your content here in Markdown.
```

## Adding a new kernel patch

Edit `kernel/index.md` and add an entry to the relevant subsystem section.
