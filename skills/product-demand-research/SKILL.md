---
name: product-demand-research
description: Use when the user wants to validate product demand using public YouTube, TikTok, and Instagram content, transcripts, and supported comments, producing pain points, objections, alternatives, and evidence-backed tests.
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

# Product Demand Research

## Overview

Use public social evidence as directional research, not market-size proof.

## Workflow

1. Define the category, customer, geography, and decision to inform.
2. Check coverage and search with `/v1/youtube/search`, `/v1/youtube/search/hashtag`, `/v2/instagram/reels/search`, or `/v1/instagram/search/hashtag`.
3. Gather detail/transcripts and supported YouTube or Instagram comments.
4. Code repeated pains, desired outcomes, workarounds, alternatives, objections, urgency, and purchase language.
5. Triangulate across creators and platforms. Report evidence against the idea as prominently as supporting evidence.

## Output Format

Return: Verdict, Scope and Sample, Pain Points, Desired Outcomes, Existing Alternatives, Objections, Demand Signals, Voice of Customer, Messaging Angles, Product Tests, Confidence, and Sources.

## Common Guardrails

- Use `socialscrape-api` for exact parameters, MCP tool names, CLI grammar, errors, and pagination.
- Check `/meta/coverage` before planning live calls; HTTP 501 is a capability result, never permission to invent data.
- Use only public data and cite source URLs.
- Report sampling and platform limitations.
