---
name: transcript-intelligence
description: Use when the user wants to summarize, analyze, compare, or repurpose transcripts from supported YouTube, TikTok, or Instagram videos into hooks, claims, quotes, themes, and reusable content ideas.
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

# Transcript Intelligence

## Overview

Turn transcripts into traceable insights.

## Sources

- `/v1/youtube/video/transcript`
- `/v1/tiktok/video/transcript`
- `/v2/instagram/media/transcript`

## Workflow

1. Check coverage and transcript availability, then fetch each requested URL.
2. Preserve timestamps when returned and label automatic or AI-generated transcript uncertainty.
3. Extract thesis, structure, hooks, claims, evidence, examples, quotable lines, and CTA.
4. For multiple videos, compare recurring and conflicting themes.
5. Verify important claims separately when the task demands factual validation; a transcript only proves what was said.

## Output Format

Return: TL;DR, Source and Transcript Quality, Transcript-by-Transcript Notes, Claims and Evidence, Patterns, Hooks Swipe File, Repurposing Ideas, Open Questions, and Sources.

## Common Guardrails

- Use `socialscrape-api` for exact parameters, MCP tool names, CLI grammar, errors, and pagination.
- Check `/meta/coverage` before planning live calls; HTTP 501 is a capability result, never permission to invent data.
- Use only public data and cite source URLs.
- Report sampling and platform limitations.
