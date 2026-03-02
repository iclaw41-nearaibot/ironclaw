---
name: social-monitor
version: 0.1.0
description: Social media monitoring skill. Read and analyse Twitter/X posts, Facebook, Reddit, TikTok trends. Find business opportunities, trending products, and market signals from social data.
activation:
  patterns:
    - "monitor.*social"
    - "read.*tweet"
    - "twitter.*"
    - "facebook.*post"
    - "reddit.*"
    - "tiktok.*trend"
    - "social.*media"
    - "trending.*"
    - "viral.*"
  keywords:
    - "twitter"
    - "tweet"
    - "facebook"
    - "reddit"
    - "tiktok"
    - "social"
    - "trending"
    - "viral"
    - "post"
    - "mention"
    - "hashtag"
    - "monitor"
  max_context_tokens: 3000
---

# Social Media Monitoring Skill

You monitor social media platforms to find business opportunities, trending products, market signals, and leads for Simon.

## Platforms & What to Look For

### Twitter/X
- Trending hashtags in e-commerce, dropshipping, crypto niches
- Complaints about products = opportunity to solve
- Viral products = potential dropshipping winners
- Influencer recommendations in target niches
- Tools: Apify Twitter scraper, gopher-mcp-server

### Reddit
- **r/entrepreneur** — startup ideas, pain points, tool recommendations
- **r/dropshipping** — what's working, supplier issues, winning products
- **r/sidehustle** — new income ideas
- **r/ecommerce** — platform news, strategies
- **r/algotrading, r/CryptoCurrency** — trading signals
- Look for: repeated complaints, viral posts, "I wish someone made X"
- Tools: Apify Reddit scraper, Reddit API

### Facebook
- Facebook Marketplace trends — what sells locally
- Facebook Groups in target niches
- Ad library — what competitors are advertising
- Tools: Apify Facebook scraper

### TikTok
- "TikTok made me buy it" content = dropshipping winners
- Trending sounds + products = ad creative ideas
- Fast-moving trends = early mover advantage
- Tools: Apify TikTok scraper

## Opportunity Scoring Framework
Score each opportunity 1-5 on:
1. **Demand** — clear evidence people want this
2. **Competition** — is the market winnable?
3. **Margin** — can we make money?
4. **Speed** — how fast to revenue?
5. **Simon fit** — matches his skills and resources?

**Only surface opportunities scoring 18+/25**

## Signal Types to Flag Immediately
- Product mentioned positively 3+ times in 24 hours
- Competitor outage or negative press
- New regulation affecting crypto/e-commerce
- Viral content with no clear commercial solution yet
- Influencer with 100k+ followers recommending a niche product

## Apify Integration
Use Apify MCP tools for scraping:
- `apify/twitter-scraper` — Twitter posts and trends
- `apify/reddit-scraper` — Reddit posts and comments
- `apify/facebook-pages-scraper` — Facebook page content
- `apify/tiktok-scraper` — TikTok trends and posts
- `apify/google-search-scraper` — Google trends and results
