---
title: "Vibe Coding Day 1: Building a Pinterest Nail Art Crawler with Claude"
date: 2026-03-04 09:00:00 +0900
categories: [Vibe Coding, Web Crawling with Claude]
tags: [claude, python, playwright, notion, automation, nail art]
description: My first day of vibe coding — scraping Pinterest nail art images into Notion using Claude as my coding partner.
---

## Today's Goal

Get two automation tools working before end of day:
1. Pinterest nail art scraper → Notion
2. Etsy nail tip market tracker → Excel + Notion

---

## Big 3 Tasks

| # | Task | Estimated | Actual |
|---|------|-----------|--------|
| 1 | Pinterest scraper + Notion integration | 1 hr | **1.5 hrs** |
| 2 | Etsy market tracker | 1 hr | 1 hr |
| 3 | Debug + test both scripts | 30 min | ongoing |

---

## Pinterest Nail Art Scraper

### What It Does

- Searches Pinterest for nail art keywords (french nails, gel nails, korean nail art...)
- Auto-classifies each pin by **color** and **pattern** using keyword matching
- Saves to Notion — with duplicate detection so re-running doesn't create repeat entries

### Tools

- **Claude** — wrote the entire script through conversation
- **Python + Playwright** — headless browser to scroll and scrape
- **Notion API** — saves each pin as a database entry with cover image

### Where Time Actually Went

Estimated an hour. Took an hour and a half.

The extra 30 minutes was almost entirely spent figuring out **what Pinterest actually shows in search results** — the HTML structure, which elements contain the pin ID, image URL, and alt text. Pinterest doesn't make this easy.

The other time sink was SEO — understanding which search queries actually surface the kind of nail art I wanted to collect. Turns out `"nail art design"` and `"press on nail design"` pull very different results. I ended up with 9 different search queries to cover the styles I care about.

Claude wrote the code quickly. The real work was me figuring out *what* to ask for.

### Bugs I Hit

- Notion API throws a validation error if a URL field is empty string — has to be `None`
- Database property names are **case-sensitive** — `PinID` ≠ `Pinid`
- `@import "main"` in the CSS file broke the blog build (unrelated, but painful)

### What I Learned

Vibe coding with Claude is fast, but it's not magic. I still had to:
- Read every error message carefully
- Understand enough to explain the problem back to Claude
- Make judgment calls on things Claude couldn't know (which search terms I actually wanted)

The back-and-forth felt natural though — more like pair programming than just copy-pasting code.

---

## What's Next

- [ ] Etsy API approval still pending — waiting on that
- [ ] In the meantime: analyze the Pinterest images I've collected
- [ ] Possibly build an image analysis tool using the collected data
- [ ] Add save count / popularity metric to Pinterest pins
- [ ] Schedule both scripts to run weekly automatically

---

## Honest Take

First day of actually building something with AI as a coding partner — not just using AI to answer questions, but having a full conversation that results in working code.

It's different from what I expected. The AI part is genuinely fast. The human part (knowing what you want, reading errors, making decisions) still takes real time and thought.

But compared to doing this alone? Not even close. I would have given up on the Notion API debugging alone.
