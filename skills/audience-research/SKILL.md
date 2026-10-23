---
name: audience-research
description: Use when the user wants to evaluate a creator, influencer, or brand audience from public YouTube, TikTok, or Instagram signals and produce an evidence-backed market, sponsorship, or content-fit assessment.
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

# Audience Research

## Overview

Evaluate audience fit using only public proxies. SocialScrape does not provide private audience demographics or follower lists.

## Sources

- Profiles: `/v1/youtube/channel`, `/v1/tiktok/profile`, `/v1/instagram/profile`
- Region proxy: `/v1/tiktok/profile/region`
- Content: `/v1/youtube/channel-videos`, `/v1/youtube/channel/shorts`, `/v3/tiktok/profile/videos`, `/v2/instagram/user/posts`, `/v1/instagram/user/reels`
- Public comments: `/v1/youtube/video/comments`, `/v2/instagram/post/comments`

## Workflow

1. Check `/meta/coverage`, then obtain current schemas from `/openapi.json`.
2. Pull profiles and a representative recent-content sample.
3. Inspect language, location disclosures, topics, engagement, comment language, and recurring community vocabulary.
4. Separate observed facts from inferred audience traits. Never claim age, gender, follower geography, or authenticity without direct evidence.
5. Score target-market fit and state sample size and confidence.

## Output Format

Return a Markdown brief with: Fit Summary, Public Evidence, Audience Proxies, Content and Community Fit, Risks, Recommendation, Confidence, and Sources.

## Common Guardrails

- Use `socialscrape-api` for exact parameters, MCP tool names, CLI grammar, errors, and pagination.
- Check `/meta/coverage` before planning live calls; HTTP 501 is a capability result, never permission to invent data.
- Use only public data and cite source URLs.
- Report sampling and platform limitations.
