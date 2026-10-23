---
name: content-repurposing
description: Use when the user wants to turn supported YouTube, TikTok, or Instagram videos, posts, and transcripts into platform-ready content assets while preserving source meaning and attribution.
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

# Content Repurposing

## Overview

Transform source material without inventing claims.

## Sources

Use `/v1/youtube/video/transcript`, `/v1/tiktok/video/transcript`, or `/v2/instagram/media/transcript`; enrich with `/v1/youtube/video`, `/v2/tiktok/video`, or `/v1/instagram/post` when needed.

## Workflow

1. Check coverage and fetch the detail and/or transcript.
2. Extract thesis, evidence, hooks, stories, quotable lines, and calls to action.
3. Distinguish direct quotes from paraphrases and retain source links.
4. Adapt length, opening, structure, and CTA to each requested destination.
5. Flag uncertain transcript passages instead of silently correcting substantive details.

## Output Format

Return: Source Material, Core Thesis, Content Atoms, requested assets, Suggested CTAs, Fact/Quote Checks, and Sources. Do not imply the original creator endorsed derivative wording.

## Common Guardrails

- Use `socialscrape-api` for exact parameters, MCP tool names, CLI grammar, errors, and pagination.
- Check `/meta/coverage` before planning live calls; HTTP 501 is a capability result, never permission to invent data.
- Use only public data and cite source URLs.
- Report sampling and platform limitations.
