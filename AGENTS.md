# SocialScrape Social Media Research Skills Repo

This repository contains agent skills for public YouTube, TikTok, and Instagram research through SocialScrape.

## Routing

Use the narrowest workflow skill that matches the requested deliverable. Use `socialscrape-api` as the raw endpoint-routing skill. If a workflow needs endpoint details, read `skills/socialscrape-api/SKILL.md` rather than guessing.

Before calling an endpoint, fetch `/meta/coverage` and the deployment's `/openapi.json`; do not assume catalog presence means implementation. Only YouTube, TikTok, and Instagram are in scope. An HTTP 501 is a supported capability result, not a reason to invent data.

## Contribution Rules

- Keep each skill at `skills/<name>/SKILL.md`; make frontmatter `name` equal the directory.
- Use `SOCIALSCRAPE_API_KEY`, `SOCIALSCRAPE_BASE_URL`, and `https://scrape.mimic.host`.
- Reference only paths in the 66-route SocialScrape catalog and clearly label fallback-dependent paths.
- Keep outputs sourced, public-data-only, platform-aware, and explicit about samples and confidence.
- Do not add credit warnings for native SocialScrape requests. Discuss rate, caching, latency, and fallback provenance instead.
- Preserve MIT attribution for adapted ScrapeCreators material.

## Validate

```bash
python3 scripts/validate-skills.py
git diff --check
```
