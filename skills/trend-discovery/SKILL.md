---
name: trend-discovery
description: Use when the user wants to discover emerging content trends on YouTube, TikTok, or Instagram and produce evidence, examples, lifecycle assessment, and actionable content tests without overstating unsupported trending data.
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

# Trend Discovery

## Overview

Identify repeated patterns from supported search and content samples. Native dedicated trending feeds are generally unavailable.

## Sources

Use `/v1/youtube/search`, `/v1/youtube/search/hashtag`, `/v2/instagram/reels/search`, `/v1/instagram/search/hashtag`, `/v1/instagram/search/popular`, and known TikTok profiles/sounds via `/v3/tiktok/profile/videos`, `/v1/tiktok/song`, and `/v1/tiktok/song/videos`.

## Workflow

1. Define niche, region, time window, and what counts as a trend.
2. Check coverage; do not route normal work to compatibility-only TikTok trending/search or YouTube trending Shorts unless fallback is known to be enabled.
3. Gather examples and dates, then cluster repeated topics, sounds, hooks, formats, and visual structures.
4. Assess velocity, recurrence, cross-creator spread, saturation, and brand fit.
5. Label each finding emerging, growing, saturated, or uncertain and state the evidence.

## Output Format

Return: Trends Worth Acting On, Evidence and Examples, Sounds/Hashtags/Formats, Lifecycle, Content Tests, Watchlist, Caveats, and Sources.

## Common Guardrails

- Use `socialscrape-api` for exact parameters, MCP tool names, CLI grammar, errors, and pagination.
- Check `/meta/coverage` before planning live calls; HTTP 501 is a capability result, never permission to invent data.
- Use only public data and cite source URLs.
- Report sampling and platform limitations.
