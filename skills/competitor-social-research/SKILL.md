---
name: competitor-social-research
description: Use when the user wants to compare competitors across YouTube, TikTok, and Instagram and produce a sourced brief on positioning, content patterns, outliers, gaps, and recommended tests.
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

# Competitor Social Research

## Overview

Compare like with like across supported platforms.

## Sources

Use profile and feed routes: `/v1/youtube/channel`, `/v1/youtube/channel-videos`, `/v1/youtube/channel/shorts`, `/v1/tiktok/profile`, `/v3/tiktok/profile/videos`, `/v1/instagram/profile`, `/v2/instagram/user/posts`, `/v1/instagram/user/reels`.

## Workflow

1. Define competitors, platforms, time window, and comparison dimensions.
2. Check `/meta/coverage` and `/openapi.json`; gather comparable profile and content samples.
3. Normalize metrics within each platform and content type; do not compare raw Shorts views directly with Instagram engagement.
4. Identify positioning, recurring pillars, hooks, formats, cadence, outliers, and white space.
5. Turn evidence into a small set of testable recommendations.

## Output Format

Return: Executive Summary, Method and Sample, Competitor Snapshot, What Works by Competitor, Cross-Competitor Patterns, Gaps, Recommended Tests, Caveats, and Sources.

## Common Guardrails

- Use `socialscrape-api` for exact parameters, MCP tool names, CLI grammar, errors, and pagination.
- Check `/meta/coverage` before planning live calls; HTTP 501 is a capability result, never permission to invent data.
- Use only public data and cite source URLs.
- Report sampling and platform limitations.
