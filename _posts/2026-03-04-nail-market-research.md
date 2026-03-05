---
title: "Small Biz Day 1: Nail Tip Market Research on Etsy"
date: 2026-03-04 10:00:00 +0900
categories: [Small Biz, Market Research]
tags: [nail, etsy, market research, automation, python, small business, canada]
description: Day one of researching the nail tip market on Etsy
---

## Today's Goal

Understand the nail tip market on Etsy well enough to know:
- Who's selling, and how well
- What price range works
- What styles are actually moving

And automate it so I can keep tracking over time.

---

## Big 3 Tasks

| # | Task | Estimated | Actual |
|---|------|-----------|--------|
| 1 | Etsy API setup + approval | 30 min | **waiting** |
| 2 | Build shop tracker script | 1 hr | 1 hr |
| 3 | Analyze top 10 shops | 30 min | pending API |

---

## What I Built

An automated Etsy tracker that:
- Searches 12 nail tip keywords across Etsy
- Aggregates results by shop
- Scores each shop by sales volume, favorites, and listing count
- Pulls top 10 shops and saves everything to Excel + Notion

The Excel file has three sheets:
- **Dashboard** — current top 10 rankings
- **History** — cumulative data every time I run it (tracks ranking changes over time)
- **Product List** — top 5 products per shop by favorites

### Why Automate This

Manually checking 10 shops every week across 12 keyword searches would take hours. This runs in under 10 minutes and logs everything automatically.

---

## What I Found (So Far)

API approval is still pending so I haven't pulled real data yet.

But from manual browsing while waiting:
- Press-on sets in the **$15–$25 range** seem to have the most reviews
- **Short and medium lengths** are outperforming long nails lately
- Shops with cohesive visual branding (consistent photo style) look significantly more professional
- **French and nude** styles are evergreen — always in demand

Will update this post once the API is live and I have real numbers.

---

## The API Question

Etsy's developer terms technically restrict using the API for competitor analysis. I spent time thinking about this before proceeding.

My read: I'm an individual doing personal market research before starting a shop of my own — not building a commercial analytics product. The risk of account action at this scale is low. But it's worth knowing the rules exist.

---

## What's Next

- [ ] Etsy API approval → run the tracker for real data
- [ ] Analyze Pinterest images collected yesterday → spot style trends
- [ ] Possibly build an image analysis tool to categorize what I've collected
- [ ] Start thinking about first product lineup based on findings

---

## Honest Take

Starting a business while job hunting in a new country is a lot.

The automation side actually helps with the anxiety — instead of endlessly browsing Etsy and spiraling, I built something that does the browsing for me and gives me structured data. Feels more in control.

Whether the nail business goes anywhere or not, the process of researching it properly (and building tools to do it) is already teaching me things I wouldn't have learned otherwise.

That feels like enough of a reason to keep going.
