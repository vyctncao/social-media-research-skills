---
name: socialscrape-api
description: >-
  Scrape and extract public YouTube, TikTok, and Instagram data using the
  SocialScrape REST API, MCP server, or client CLI. Use when the user asks to
  fetch, extract, search, or look up supported profiles, channels, posts,
  videos, reels, comments, transcripts, playlists, highlights, hashtags,
  sounds, live streams, or engagement metrics, or mentions SocialScrape or a
  ScrapeCreators-compatible API for these platforms.
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
    tags: [scraping, social-media, socialscrape, tiktok, instagram, youtube, creator-data, transcripts]
---

# SocialScrape API

Scrape and extract public data from YouTube, TikTok, and Instagram through a self-hosted, ScrapeCreators-compatible API. This deployment exposes 66 compatible endpoint paths; 37 are implemented locally and unsupported routes return HTTP 501 unless the server owner configured ScrapeCreators fallback.

**Base URL:** `${SOCIALSCRAPE_BASE_URL:-https://scrape.mimic.host}`

## How to Call

All API endpoints use GET requests and return JSON. Pass `x-api-key: $SOCIALSCRAPE_API_KEY`. Never print or persist the key.

```bash
BASE_URL="${SOCIALSCRAPE_BASE_URL:-https://scrape.mimic.host}"
curl -sG "$BASE_URL/v1/tiktok/profile" \
  --data-urlencode "handle=stoolpresidente" \
  -H "x-api-key: $SOCIALSCRAPE_API_KEY"
```

```javascript
const baseUrl = process.env.SOCIALSCRAPE_BASE_URL ?? "https://scrape.mimic.host";
const url = new URL("/v1/tiktok/profile", baseUrl);
url.searchParams.set("handle", "stoolpresidente");
const res = await fetch(url, { headers: { "x-api-key": process.env.SOCIALSCRAPE_API_KEY } });
const data = await res.json();
```

## Capability and API Schema

Before planning a multi-step workflow, fetch authenticated `GET /meta/coverage` and check every route's status and limitations. Fetch `GET /openapi.json` for current parameter and response schemas. Human-readable documentation is at `/app/docs`. Catalog presence does not imply native implementation.

## Endpoint Catalog

All 66 catalog routes are listed below. Native routes run locally through SocialScrape. Fallback-dependent routes normally return 501, but a server owner may configure ScrapeCreators fallback.

### Instagram — native (12)

| Intent | REST path | Required/core parameters | Notes |
|---|---|---|---|
| Post/Reel detail | `/v1/instagram/post` | `url` | Logged-out data; anonymous play count may be absent |
| Profile | `/v1/instagram/profile` | `handle` | First 12 slim post nodes |
| Profile post count | `/v1/instagram/profile/post-count` | `handle`; `allow_estimated` optional | Can return 422 `estimate_only` |
| Hashtag posts | `/v1/instagram/search/hashtag` | `hashtag` | First page; later cursor may be unsupported |
| Popular search | `/v1/instagram/search/popular` | `query` | First page |
| Highlight detail | `/v1/instagram/user/highlight/detail` | `id` | Public availability only |
| Profile highlights | `/v1/instagram/user/highlights` | `user_id` or `handle` | First 10 |
| Profile reels | `/v1/instagram/user/reels` | `user_id` or `handle` | First 12; later `max_id` unsupported |
| Transcript | `/v2/instagram/media/transcript` | `url` | Requires configured local Whisper |
| Post comments | `/v2/instagram/post/comments` | `url` | Usually first ~15; later cursor unsupported |
| Reels search | `/v2/instagram/reels/search` | `query` | First page; later `page` unsupported |
| Profile posts | `/v2/instagram/user/posts` | `handle` | First 12; later `next_max_id` unsupported |

### TikTok — native (10)

| Intent | REST path | Required/core parameters | Notes |
|---|---|---|---|
| Collection videos | `/v1/tiktok/collection/videos` | `url` | `cursor` supported |
| Live room | `/v1/tiktok/live` | `room_id`, `user_id` | May be blocked upstream |
| Profile | `/v1/tiktok/profile` | `handle` or `user_id` | Public profile |
| Profile region | `/v1/tiktok/profile/region` | `handle` | Depends on original sound/app API |
| Sound detail | `/v1/tiktok/song` | `clipId` | App API can be unstable |
| Sound videos | `/v1/tiktok/song/videos` | `clipId`; `cursor` optional | App API can be unstable |
| User live | `/v1/tiktok/user/live` | `handle` | JS challenge may return 503 |
| Transcript | `/v1/tiktok/video/transcript` | `url` | Native captions; optional local fallback |
| Video detail | `/v2/tiktok/video` | `url` | Photo posts supported |
| Profile videos | `/v3/tiktok/profile/videos` | `handle`; `max_cursor` optional | `popular` sort and excluding pinned unsupported |

### YouTube — native (15)

| Intent | REST path | Required/core parameters | Notes |
|---|---|---|---|
| Channel | `/v1/youtube/channel` | one of `channelId`, `handle`, `url` | Email is null |
| Channel videos | `/v1/youtube/channel-videos` | `channelId` or `handle` | Exact hyphenated path |
| Community feed | `/v1/youtube/channel/community-posts` | `channelId` or `handle` | `continuationToken` supported |
| Live tab | `/v1/youtube/channel/lives` | `channelId` or `handle` | `continuationToken` supported |
| Playlists tab | `/v1/youtube/channel/playlists` | `channelId` or `handle` | `continuationToken` supported |
| Shorts tab | `/v1/youtube/channel/shorts` | `channelId` or `handle` | `continuationToken` supported |
| Community post | `/v1/youtube/community-post` | `url` | Text, image, poll, video, shares |
| Playlist | `/v1/youtube/playlist` | `playlist_id` | Mixes rejected; continuation supported |
| Search | `/v1/youtube/search` | `query` | Paid-promotion filter unsupported |
| Hashtag search | `/v1/youtube/search/hashtag` | `hashtag` | `type=all|shorts` |
| Video/Short | `/v1/youtube/video` | `url` | Anonymous restrictions may return 403 |
| Comment replies | `/v1/youtube/video/comment/replies` | `continuationToken` | Token comes from comments |
| Comments | `/v1/youtube/video/comments` | `url` | `order=top|newest` |
| Sponsors | `/v1/youtube/video/sponsors` | `url` | Mostly heuristic |
| Transcript | `/v1/youtube/video/transcript` | `url` | Language selection supported |

## Unsupported Compatibility Paths

### Instagram — fallback-dependent (8)
`/v1/instagram/audio/reels`, `/v1/instagram/basic-profile`, `/v1/instagram/post/comment/replies`, `/v1/instagram/reels/trending`, `/v1/instagram/search`, `/v1/instagram/search/profiles`, `/v1/instagram/user/embed`, `/v1/instagram/user/tagged-posts`

### TikTok — fallback-dependent (19)
`/v1/tiktok/ad-library/ad`, `/v1/tiktok/ad-library/search`, `/v1/tiktok/creators/popular`, `/v1/tiktok/get-trending-feed`, `/v1/tiktok/product`, `/v1/tiktok/search/hashtag`, `/v1/tiktok/search/keyword`, `/v1/tiktok/search/suggestions`, `/v1/tiktok/search/top`, `/v1/tiktok/search/users`, `/v1/tiktok/shop/product/reviews`, `/v1/tiktok/shop/products`, `/v1/tiktok/shop/search`, `/v1/tiktok/user/audience`, `/v1/tiktok/user/followers`, `/v1/tiktok/user/following`, `/v1/tiktok/user/showcase`, `/v1/tiktok/video/comment/replies`, `/v1/tiktok/video/comments`

### YouTube — fallback-dependent (2)
`/v1/youtube/search/typeahead`, `/v1/youtube/shorts/trending`

## Pagination

Pass the previous response's token unchanged and stop when the next token is null or absent.

- YouTube: `continuationToken`
- TikTok profile videos: `max_cursor`; sound/collection videos: `cursor`
- Instagram posts: `next_max_id`; reels: `max_id`; comments/search: `cursor` or `page` (later pages generally unsupported natively)

Tokens may be native or opaque values beginning `ss1.`. Never decode them. A malformed token returns 400 `bad_cursor`.

## Responses and Errors

Success fields are top-level:

```json
{"success": true, "credits_charged": 0}
```

Cache hits add `"cached": true` and `"cached_at": "<timestamp>"`. Errors use:

```json
{"success": false, "error": "<code>", "message": "<human-readable message>"}
```

- 400: fix parameters/cursor; 401: correct the API key; 403: private/login/age/geo restriction.
- 404: absent resource or out-of-scope path; 405: use GET; 422: accept Instagram count estimates only if appropriate.
- 500: configuration/transcription needs server action; retry only transient timeout errors.
- 501: unsupported or transcription unavailable; report it, do not fabricate.
- 502/503: bounded retries with jitter (1s, 2s, 4s), then report proxy/rate-limit/bot-check failure.

Use `cache_max_age` (`1d`, `3d`, `7d`, `14d`, `30d`, or hours such as `12h`) to reduce duplicate work and platform pressure.

## Cost, Rate, and Latency

SocialScrape charges no credits; locally served successes report `credits_charged: 0`. Optimize for server capacity and upstream rate limits rather than credits. Detail/profile calls are usually faster than transcription and broad paginated research. Cache stable data, paginate deliberately, cap retries, and tell the user when long transcription may add latency.

Configured ScrapeCreators fallback can consume the server owner's credits and adds `x-socialscrape-fallback: scrapecreators`. Never request or expose the owner's fallback key; disclose fallback-sourced results.

## MCP

The MCP endpoint is `${SOCIALSCRAPE_BASE_URL:-https://scrape.mimic.host}/mcp` and authenticates with `x-api-key` or an OAuth bearer token. Every catalog path is a tool. Convert a path by removing the leading slash and replacing `/` and `-` with `_`:

- `/v1/youtube/channel-videos` → `v1_youtube_channel_videos`
- `/v2/instagram/post/comments` → `v2_instagram_post_comments`
- `/v3/tiktok/profile/videos` → `v3_tiktok_profile_videos`

Call with the same query argument names as REST. MCP returns pretty-printed endpoint JSON as text and marks non-2xx results with `isError: true`. Use `tools/list` or `/openapi.json` for exact schemas, and check `/meta/coverage` before fallback-dependent tools.

## CLI

The client grammar is `socialscrape <platform> <command> [flags]`; global output flags go before the platform command. Examples:

```bash
socialscrape youtube channel-videos --handle MrBeast
socialscrape tiktok profile-videos --handle stoolpresidente --max-cursor '<token>'
socialscrape instagram post-comments --url 'https://www.instagram.com/reel/SHORTCODE/'
socialscrape --json youtube search --query 'creator economy'
```

CLI command names flatten the path after the platform with hyphens: `channel/community-posts` becomes `channel-community-posts`; version prefixes are omitted. Flags kebab-case parameter names except compatibility spellings retained by help, such as `--channelId`, `--continuationToken`, and `--clipId`. Run `socialscrape list [platform]` or `<command> --help` rather than guessing. Configure with `SOCIALSCRAPE_API_KEY` and optional `SOCIALSCRAPE_BASE_URL`.
