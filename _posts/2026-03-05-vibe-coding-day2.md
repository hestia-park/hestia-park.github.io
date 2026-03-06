---
title: "Vibe Coding Day 2: AI Image Automation, News Bot & ComfyUI"
date: 2026-03-05 09:00:00 +0900
categories: [Vibe Coding, Day Log]
tags: [claude, comfyui, stable diffusion, gemini, slack, notion, ticktick, github pages]
description: Set up the blog, built a morning briefing bot with news + tasks, and got ComfyUI running for AI image generation.
---

## What I Did Today

Three main things:

1. **AI Image Generation Automation** — ComfyUI setup + prompt optimizer with Gemini scoring
2. **Economy News & Daily Task Bot** — Morning Slack briefing with Canadian news + TickTick tasks
3. **ComfyUI Test** — First images generated, troubleshooting diptych issues

---

## Big 3 Tasks

| # | Task | Estimated | Actual | Status |
|---|------|-----------|--------|--------|
| 1 | GitHub Pages blog setup | 1 hr | 2 hr | ✅ Done (with a lot of debugging) |
| 2 | Morning briefing Slack bot | 1 hr | 1.5 hr | ✅ Done |
| 3 | ComfyUI image generation | 1 hr | ongoing | 🔄 In progress |

---

## 1. GitHub Pages Blog Setup

### Why

Was using Hydejack Pro theme before — but it's no longer available for free. Rather than paying for a license on a blog I barely maintained, I decided to switch to Chirpy which is open source and actively maintained.

### Hydejack Pro vs Chirpy

| | Hydejack Pro | Chirpy |
|--|--|--|
| Cost | Paid license required | Free / Open source |
| Setup complexity | High | Low |
| Maintenance | Limited updates | Actively maintained |
| Mobile support | Good | Excellent |
| Search | Manual config | Built-in |
| Dark mode | Manual | Toggle built-in |
| Post structure | Complex | Simple front matter |
| Best for | Premium personal blogs | Dev blogs, documentation |

### Troubleshooting

| Error | Cause | Fix |
|-------|-------|-----|
| `jekyll-feed` LoadError | Added `plugins:` block to `_config.yml` — conflicted with Chirpy's internal management | Removed the entire plugins block |
| `@import "main"` deprecated | Unnecessary import line in CSS file | Removed that line |
| `assets/assets/css` double path | Wrong file path when creating via GitHub web UI | Recreated at correct path |
| Tags internal link errors | htmlproofer checking `/tags/` URLs that don't pre-exist | Excluded `/tags/` and `/categories/` from htmlproofer in workflow yml |
| Avatar file missing | Path set in `_config.yml` but no file uploaded | Set `avatar: ""` temporarily |
| Social links error | `'a' tag missing reference` — empty links array | Added GitHub profile link |

> Most fixes today were "just delete it" solutions. Next time I want to dig deeper before removing — there are usually better alternatives than stripping things out.

---

## 2. Morning Briefing Bot (News + TickTick)

### Why

Canadian economic news isn't just background noise for me right now — it's one of the best ways to understand what services and products people actually need, which directly feeds into business decisions. As someone job hunting here, staying on top of market trends matters.

Adding TickTick tasks to the same message made sense: if I'm already checking Slack in the morning, having AI reprioritize my day at the same time cuts out one more decision.

### How It Works

![Morning Briefing Flow](/assets/img/posts/AI-Daily-Automation-Workflow.png)

### Slack Message Structure

```
🌅 Morning Briefing — March 5, 2026
────────────────────────────────
📰 Top 5 Canadian Economy News
  🍁 #1 | CBC Business
  💼 #2 | Financial Post
  ...
────────────────────────────────
🎯 Today's Big 3 (AI Recommended)
  1. [task] ← due today
  2. [task] ← high priority
  3. [task]
────────────────────────────────
🤖 AI Advice
  "Focus on the deadline task first..."
```

### Troubleshooting

| Error | Cause | Fix |
|-------|-------|-----|
| Gemini 404 Not Found | `gemini-1.5-flash` was deprecated in April 2025 | Switched to `gemini-2.0-flash` |
| 429 Too Many Requests | Hit per-minute limit during repeated test runs | Added auto-retry with 60s/120s/180s backoff |
| RSS feed hanging forever | No timeout set — stuck on unresponsive feeds | Added `requests.get(timeout=10)` + skip on timeout |

---

## 3. ComfyUI Image Generation

### Why

Testing AI image generation for Adobe Stock. With M2 24GB running locally, generation cost is basically zero. Gemini handles prompt creation on the free tier.

Tried AUTOMATIC1111 first — kept hitting a CLIP installation error on M2 that I couldn't get past. Switched to ComfyUI and it worked immediately.

### Node Flow

![ComfyUI Workflow](/assets/img/posts/ComfyUI-Workflow-Diagram.png)

### First Results

Both test images had the same issue: **two people in the frame** (diptych effect) even though the prompt asked for one person.

**Root cause**: SDXL tends to fill empty space in office scenes by duplicating the subject.

**Fix — strengthened negative prompt:**
```
duplicate, cloned, two people, diptych,
collage, mirror, split image,
revealing clothes, open shirt, cleavage
```

**Also added to positive prompt:** `solo`, `single subject`

### Sampler Reference

| Sampler | Scheduler | Speed | Quality | Best for |
|---------|-----------|-------|---------|---------|
| `euler` | `normal` | ⚡⚡⚡ | OK | Quick testing |
| `dpmpp_2m` | `sgm_uniform` | ⚡⚡ | Good | Balanced |
| `dpmpp_2m` | `karras` | ⚡⚡ | High | Current setting |
| `dpmpp_2s_ancestral` | `karras` | ⚡ | High | Portrait detail |

---

## 4. Prompt Optimizer (In Progress)

### Structure

| Round | Prompts | Images each | Resolution | Gemini calls |
|-------|---------|-------------|------------|--------------|
| Round 1 | 10 | 3 | 1024px | 10 |
| Round 2 | Top 5 | 5 | 1024px | 5 |
| Round 3 | Top 3 | 10 | 2048px | 3 |
| **Total** | | **85 images** | | **18 calls** |

Gemini analyzes each batch of images together (not one by one), scores them, identifies issues, and returns an improved prompt for the next round. Results log automatically to Notion.

---

## What I Learned

**Chirpy**: Don't declare plugins manually in `_config.yml` — Chirpy manages its own dependencies internally.

**ComfyUI vs AUTOMATIC1111**: On M2 Mac, ComfyUI is significantly more stable. AUTOMATIC1111 kept failing at the CLIP install step with no clean fix.

**Gemini model names expire**: Always verify the current model name. `gemini-1.5-flash` was already gone.

**Vibe coding reality**: Claude writes code fast. But reading error messages, understanding what went wrong, and explaining it back clearly — that's still entirely on me. It takes more active thinking than I expected.

---

## What's Left

- [ ] Actually run `prompt_optimizer.py` end-to-end
- [ ] Set up Notion DB properties for prompt optimizer
- [ ] Test TickTick OAuth first authentication
- [ ] Verify morning briefing bot Slack delivery
- [ ] Create Adobe Stock contributor account
- [ ] Upload avatar image to blog
