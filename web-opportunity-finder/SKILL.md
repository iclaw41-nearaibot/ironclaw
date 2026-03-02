---
name: web-opportunity-finder
version: 0.1.0
description: Autonomous web research skill. Scrape the web to find business opportunities, trending niches, product ideas, competitor gaps, and market signals.
activation:
  patterns:
    - "find.*opportunit"
    - "research.*niche"
    - "scrape.*web"
    - "market.*research"
    - "competitor.*gap"
    - "product.*idea"
    - "trending.*niche"
  keywords:
    - "opportunity"
    - "niche"
    - "research"
    - "scrape"
    - "market"
    - "trend"
    - "competitor"
    - "gap"
    - "idea"
    - "business"
  max_context_tokens: 3000
---

# Web Opportunity Finder Skill

You autonomously research the web to find viable business opportunities for Simon.

## Research Sources (Priority Order)

### Free Sources
1. **Google Trends** — spot rising search interest before it peaks
2. **Reddit** — find pain points and unmet needs
3. **Amazon Best Sellers** — what people are buying
4. **eBay Trending** — what's selling in the UK
5. **AliExpress Hot Products** — dropshipping candidates
6. **Product Hunt** — new tools and SaaS ideas
7. **Hacker News** — tech trends and startup ideas
8. **IndieHackers** — what bootstrappers are building

### Paid/API Sources (when available)
- Google Keyword Planner — search volume data
- SemRush — competitor traffic and keywords
- Jungle Scout — Amazon product research

## Opportunity Types to Look For

### Dropshipping Products
- Rising Google Trends + low competition on Google Shopping
- Selling on AliExpress for under £5, comparable items on Amazon for £20+
- Visually demonstrable (good for video ads)
- Solves a problem or satisfies a passion

### Service Opportunities
- Repeated questions on Reddit with no good answers
- Businesses paying for something that could be automated
- Gaps in existing tools (look at 1-star reviews)

### Content/Media Opportunities
- High-volume keywords with weak existing content
- Niche communities with no dedicated resource site

## Research Process

1. **Identify seed topic** — start with Simon's interests (crypto, e-commerce, UK market)
2. **Expand** — use Google Trends to find related rising topics
3. **Validate demand** — check search volume and social discussion
4. **Check competition** — Google the main keywords, assess difficulty
5. **Estimate margin** — research product costs vs selling price
6. **Score** — apply opportunity scoring framework
7. **Report** — write a 1-page summary if score is 18+/25

## Output Format
For each opportunity found:
- **What it is** (1 sentence)
- **Evidence of demand** (data points)
- **Competition level** (low/medium/high)
- **Estimated margin** (£ or %)
- **Time to first revenue** (estimate)
- **Recommended first step**
- **Opportunity score** (/25)
