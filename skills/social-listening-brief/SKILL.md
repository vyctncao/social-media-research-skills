---
name: social-listening-brief
description: Use when the user wants to monitor a topic or brand across supported YouTube, TikTok, and Instagram public data and produce a sourced brief on themes, sentiment signals, notable content, risks, and opportunities.
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

# Social Listening Brief

## Overview

Create a bounded public-signal snapshot, not a claim of exhaustive listening.

## Sources

Use YouTube search and hashtag search, Instagram reels and hashtag search, and supported detail, transcript, profile, and comment routes. TikTok keyword/hashtag search is compatibility-only and may require fallback; profile and known-URL monitoring work natively.

## Workflow

1. Define query set, platforms, language, geography, and time window.
2. Check coverage and gather a documented sample.
3. Deduplicate cross-posts; code themes, stance, questions, risks, and opportunities.
4. Treat sentiment as an interpretation and include mixed/neutral evidence.
5. Compare only similar samples and explain blind spots.

## Output Format

Return: Executive Summary, Scope and Method, Volume/Sample Notes, Top Themes, Sentiment Signals, Notable Posts, Risks, Opportunities, Recommended Actions, Caveats, and Sources.

## Common Guardrails

- Use `socialscrape-api` for exact parameters, MCP tool names, CLI grammar, errors, and pagination.
- Check `/meta/coverage` before planning live calls; HTTP 501 is a capability result, never permission to invent data.
- Use only public data and cite source URLs.
- Report sampling and platform limitations.
