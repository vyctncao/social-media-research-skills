# Social Media Research Skills for SocialScrape

Practical AI agent skills for YouTube, TikTok, and Instagram research, powered by [SocialScrape](https://scrape.mimic.host).

These skills help agents find outlier posts, mine supported comments, summarize transcripts, research competitors, and turn public social data into useful business artifacts.

This is not just endpoint routing. The goal is to give your AI agent complete research workflows it can run across YouTube, TikTok, and Instagram using SocialScrape's ScrapeCreators-compatible API.

## Install

```bash
npx skills add vyctncao/social-media-research-skills
```

Works with Claude Code, Cursor, OpenAI Codex, GitHub Copilot, Gemini CLI, Windsurf, VS Code, and other agents that support the [Agent Skills spec](https://agentskills.io).

Install only the API skill noninteractively:

```bash
npx skills add vyctncao/social-media-research-skills --skill socialscrape-api -g -a claude-code -y
```

## Setup

Set the deployment URL and your API key:

```bash
export SOCIALSCRAPE_BASE_URL=https://scrape.mimic.host
export SOCIALSCRAPE_API_KEY=your_api_key
```

Open [scrape.mimic.host](https://scrape.mimic.host) to access the hosted SocialScrape dashboard and API documentation.

## Available Skills

| Skill | What it does |
|---|---|
| `socialscrape-api` | Routes REST, MCP, and CLI calls across the complete 66-route compatibility catalog |
| `outlier-post-finder` | Scores unusually strong YouTube, TikTok, and Instagram posts against account baselines |
| `transcript-intelligence` | Extracts hooks, claims, themes, quotes, and reuse ideas from supported transcripts |
| `comment-mining` | Mines supported YouTube and Instagram comments for themes and audience language |
| `competitor-social-research` | Compares competitors' positioning, content patterns, outliers, and gaps |
| `trend-discovery` | Finds evidence-backed trends without overstating unavailable trending feeds |
| `influencer-prospecting` | Builds ranked creator shortlists from public discovery and profile evidence |
| `audience-research` | Assesses audience fit using explicit public proxies, not private demographics |
| `social-listening-brief` | Produces a bounded topic or brand listening brief from supported public sources |
| `product-demand-research` | Finds pains, objections, alternatives, and product-demand signals |
| `creator-profile-teardown` | Reverse-engineers creator positioning, pillars, hooks, formats, and outliers |
| `content-repurposing` | Turns supported posts and transcripts into traceable derivative assets |

```text
socialscrape-api
        │
        ▼
social research workflows
 ├─ outlier-post-finder
 ├─ transcript-intelligence
 ├─ comment-mining
 ├─ competitor-social-research
 ├─ trend-discovery
 ├─ influencer-prospecting
 ├─ audience-research
 ├─ social-listening-brief
 ├─ product-demand-research
 ├─ creator-profile-teardown
 └─ content-repurposing
```

## Scope Changes from the Upstream Skills

This repository adapts ScrapeCreators' MIT-licensed workflow skills to SocialScrape's YouTube, TikTok, and Instagram scope. `ad-library-teardown` is omitted because SocialScrape has no natively implemented ad-library route. Audience research is narrowed to public proxies. Comment mining uses native YouTube and Instagram comments; TikTok comments require an owner-configured fallback. Trend discovery and creator discovery state where dedicated search or trending routes are fallback-dependent rather than promising unavailable data.

## Design Principles

1. **Workflow first** — turn endpoint results into useful decisions and artifacts.
2. **Evidence over vibes** — cite source URLs, sample sizes, dates, and confidence.
3. **Platform-aware comparisons** — do not flatten unlike metrics across platforms or formats.
4. **Public-data only** — SocialScrape extracts public YouTube, TikTok, and Instagram data. Do not promise private or logged-in data.
5. **Honest inference** — distinguish observation, interpretation, and unknowns.
6. **Actionable outputs** — end research with clear next steps or tests.
7. **Coverage-aware** — check `/meta/coverage` and describe 501 limitations before planning a workflow around an unsupported route.

## Validation

```bash
python3 scripts/validate-skills.py
git diff --check
```

## Links

- [SocialScrape](https://scrape.mimic.host)
- [API Documentation](https://scrape.mimic.host/app/docs)
- [OpenAPI Schema](https://scrape.mimic.host/openapi.json)
- [Runtime Coverage](https://scrape.mimic.host/meta/coverage)
- [Source](https://github.com/vyctncao/socialscrape)

## License

MIT. The license preserves the ScrapeCreators copyright notice for adapted upstream material and adds attribution for SocialScrape modifications.
