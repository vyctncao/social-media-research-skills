---
name: comment-mining
description: Use when the user wants to analyze public comments on supported YouTube videos or Instagram posts and produce themes, questions, objections, demand signals, and reusable audience language.
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

# Comment Mining

## Overview

Extract structured audience insights from supported public comments. TikTok comments are compatibility-only and may require configured fallback.

## Sources

- YouTube: `/v1/youtube/video/comments`, then `/v1/youtube/video/comment/replies`
- Instagram: `/v2/instagram/post/comments`

## Workflow

1. Check `/meta/coverage` and schemas. If the user asks for TikTok comments, explain the native limitation before trying a fallback-capable route.
2. Fetch comments, paginate where supported, and preserve URLs or IDs for traceability.
3. Remove obvious spam and duplicates without hiding dissent.
4. Cluster recurring themes; count the analyzed sample, not the platform's total audience.
5. Extract representative short quotes, questions, objections, buying signals, and content requests.

## Output Format

Return a Markdown report with: Summary, Sample and Method, Top Themes, Questions, Objections, Demand Signals, Exact Language, Content Ideas, Caveats, and Sources. Label inferred sentiment and avoid demographic claims.

## Common Guardrails

- Use `socialscrape-api` for exact parameters, MCP tool names, CLI grammar, errors, and pagination.
- Check `/meta/coverage` before planning live calls; HTTP 501 is a capability result, never permission to invent data.
- Use only public data and cite source URLs.
- Report sampling and platform limitations.
