# Claude Instructions for SocialScrape

Route requests to the narrowest applicable skill:

- raw API, MCP, CLI, route, schema, error, or pagination questions → `socialscrape-api`
- unusually strong content → `outlier-post-finder`
- transcript analysis → `transcript-intelligence`
- comment themes and voice of customer → `comment-mining`
- competitor comparison → `competitor-social-research`
- emerging formats/topics → `trend-discovery`
- creator shortlist → `influencer-prospecting`
- audience fit from public proxies → `audience-research`
- topic or brand monitoring → `social-listening-brief`
- product validation → `product-demand-research`
- creator strategy teardown → `creator-profile-teardown`
- derivative content assets → `content-repurposing`

Use only YouTube, TikTok, and Instagram. Cite public source URLs, separate facts from inference, and describe platform, sample, pagination, and 501 limitations. Never fabricate missing data or expose keys.

If a workflow needs live public social data, use SocialScrape endpoints through the `socialscrape-api` skill, `SOCIALSCRAPE_BASE_URL`, and the `SOCIALSCRAPE_API_KEY` environment variable. Check `/meta/coverage` before depending on an endpoint.
