## Prerequisites

To build and run this Hugo site locally, you need to have the following installed:

- [Hugo](https://gohugo.io/installation/) (Extended version)
- [Go](https://go.dev/doc/install)
- [Dart Sass](https://sass-lang.com/install/)

Without these dependencies, the site may not build correctly or some features might not work as expected.

Also, make sure you initialize and update submodules:
```bash
git submodule update --init --recursive
```

## Scheduled Publishing

Posts can be scheduled for future publication using Hugo's date-based building.

### How It Works

1. `buildFuture: false` in `hugo.yaml` tells Hugo to skip posts with future dates
2. A daily Cloudflare Pages deploy hook fires at 4:00 AM MST via cron
3. On each rebuild, any post whose `date` has passed becomes live automatically

### Scheduling a Post

Set a future date in your post frontmatter:

```yaml
---
date: '2026-03-01T09:00:00-07:00'
draft: false
title: 'Your Scheduled Post'
---
```

This post won't appear on the site until the next build after March 1st at 9:00 AM MST.

### Infrastructure

- **Build trigger:** Cloudflare Pages Deploy Hook (`scheduled-daily-build`)
- **Cron source:** Cloudflare Worker (`blog-scheduled-build`) with cron trigger `0 11 * * *` (4:00 AM MST / 11:00 UTC)
- **Config:** `buildFuture: false` in `hugo.yaml`
- **Deploy hook URL:** Stored as encrypted env var `DEPLOY_HOOK_URL` on the worker

### Setup (Cloudflare-native, no GitHub Actions)

1. **Deploy Hook:** Pages → Blog project → Settings → Builds & Deployments → Deploy Hooks
2. **Worker:** Workers & Pages → `blog-scheduled-build` → hits the deploy hook URL
3. **Cron Trigger:** Worker → Triggers → `0 11 * * *` (daily at 4:00 AM MST)

### Manual Override

To preview future posts locally:
```bash
hugo server --buildFuture
```

To force-publish all scheduled posts immediately, trigger a manual deploy in Cloudflare Pages dashboard.
