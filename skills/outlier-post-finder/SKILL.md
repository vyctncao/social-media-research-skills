---
name: outlier-post-finder
description: Use when the user wants to find unusually strong posts from YouTube, TikTok, or Instagram accounts and produce normalized outlier scores, repeatable patterns, hooks, and content ideas.
allowed-tools: Bash, Read, Write, WebFetch

version: 1.0.0
author: SocialScrape
license: MIT
homepage: https://scrape.mimic.host
repository: https://github.com/vyctncao/social-media-research-skills
metadata:
  openclaw:
    requires:
      env:
        - SOCIALSCRAPE_API_KEY
    primaryEnv: SOCIALSCRAPE_API_KEY
    homepage: https://scrape.mimic.host
    tags:
      - social-media
      - research
      - socialscrape
---

# Outlier Post Finder

## Overview

Find posts that outperform a creator's own baseline.

## Sources

- YouTube: `/v1/youtube/channel-videos`, `/v1/youtube/channel/shorts`
- TikTok: `/v3/tiktok/profile/videos`
- Instagram: `/v2/instagram/user/posts`, `/v1/instagram/user/reels`
- Detail/transcripts: `/v1/youtube/video`, `/v2/tiktok/video`, `/v1/instagram/post` and their transcript routes

## Workflow

1. Check coverage and fetch enough recent items for a useful baseline.
2. Split by platform and content type. Prefer comparable age windows.
3. Compute `outlier_score = item_primary_metric / median_primary_metric`; use a robust secondary engagement measure when available.
4. Rank, then inspect top items for hook, topic, format, length, packaging, and CTA.
5. State metric gaps and sample size; do not equate correlation with cause.

## Output Format

Return: Summary, Method, Biggest Outliers table, Repeatable Patterns, Hooks to Adapt, Content Ideas, Caveats, and Sources.

## Common Guardrails

- Use `socialscrape-api` for exact parameters, MCP tool names, CLI grammar, errors, and pagination.
- Check `/meta/coverage` before planning live calls; HTTP 501 is a capability result, never permission to invent data.
- Use only public data and cite source URLs.
- Report sampling and platform limitations.
