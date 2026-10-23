---
name: creator-profile-teardown
description: Use when the user wants to analyze a YouTube, TikTok, or Instagram creator profile and produce a teardown of positioning, content pillars, outliers, hooks, formats, and useful tests.
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

# Creator Profile Teardown

## Overview

Reverse-engineer a creator's public strategy rather than merely summarizing a profile.

## Workflow

1. Check coverage and fetch the platform profile plus recent videos/posts/reels.
2. Select a representative sample and record dates and metrics.
3. Identify positioning, promised value, audience cues, content pillars, cadence, formats, and recurring hooks.
4. Find within-platform outliers; inspect detail or transcripts only for the strongest examples.
5. Translate patterns into ethical tests, not copycat instructions.

Use only cataloged profile, feed, detail, and transcript paths from `socialscrape-api`.

## Output Format

Return: Positioning, Profile Snapshot, Content Pillars, Outlier Posts, Hook and Format Patterns, What Not to Copy, Tests to Run, Caveats, and Sources.

## Common Guardrails

- Use `socialscrape-api` for exact parameters, MCP tool names, CLI grammar, errors, and pagination.
- Check `/meta/coverage` before planning live calls; HTTP 501 is a capability result, never permission to invent data.
- Use only public data and cite source URLs.
- Report sampling and platform limitations.
