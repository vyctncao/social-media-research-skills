---
name: influencer-prospecting
description: Use when the user wants to find and rank prospective creators on YouTube, TikTok, or Instagram using supported public discovery and profile signals, with fit scores and outreach angles.
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

# Influencer Prospecting

## Overview

Build a defensible shortlist. Discovery is strongest on YouTube; TikTok user search and Instagram profile search are compatibility-only and may require fallback.

## Workflow

1. Define niche, platform, geography, size, brand-safety, and fit criteria.
2. Check coverage. Use `/v1/youtube/search`, `/v1/youtube/search/hashtag`, `/v2/instagram/reels/search`, or `/v1/instagram/search/hashtag` where appropriate.
3. Resolve candidates with platform profile routes and sample recent content.
4. Score niche fit, content quality, engagement context, consistency, geography/language proxies, and brand safety.
5. Deduplicate identities and explain evidence gaps. Never invent contact details or private demographics.

## Output Format

Return: Search Criteria, Ranked Prospects table, Evidence, Best Fits, Risks, Personalized Outreach Angles, and a CSV-ready table with handle, platform, URL, public metrics, fit score, rationale, and source links.

## Common Guardrails

- Use `socialscrape-api` for exact parameters, MCP tool names, CLI grammar, errors, and pagination.
- Check `/meta/coverage` before planning live calls; HTTP 501 is a capability result, never permission to invent data.
- Use only public data and cite source URLs.
- Report sampling and platform limitations.
