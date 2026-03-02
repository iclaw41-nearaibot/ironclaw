---
name: x-monitor
version: 0.1.0
description: Monitor target X/Twitter accounts and hashtags. Track @aiedge_, AI agent influencers, and business decision-makers. Find relevant conversations to reply to. Use Apify scraper. Surface opportunities for IronClaw self-promotion and lead generation.
activation:
  patterns:
    - "monitor.*twitter"
    - "monitor.*x"
    - "watch.*account"
    - "track.*tweet"
    - "x.*monitor"
    - "twitter.*monitor"
    - "replies.*twitter"
    - "scrape.*twitter"
  keywords:
    - "twitter"
    - "x"
    - "tweet"
    - "monitor"
    - "replies"
    - "hashtag"
    - "mention"
    - "aiedge"
    - "influencer"
  max_context_tokens: 3000
---

# X Monitor Skill

Monitor target X accounts and conversations. Find leads, reply opportunities, and signals for IronClaw promotion.

## Target Accounts to Monitor
Scraped from @aiedge_ following list (2026-03-01). AI/tech accounts only.

### Tier 1 — High-value AI/agent contacts
- @OfficialLoganK (Logan Kilpatrick) — Google AI Studio, Gemini API — 280K followers
- @JonathanRoss321 (Jonathan Ross) — Chief Software Architect Nvidia, Founder of Groq — 48K followers
- @rough__sea (Ryan Dahl) — Creator of Node.js, co-founder Deno — 40K followers
- @MillionInt (Jerry Tworek) — ex-VP RL at OpenAI (o3, o1, GPT4, Codex) — 31K followers
- @lmcintosh (Lane McIntosh) — ML at Tesla Autopilot — 1.9K followers

### Tier 2 — Large influencers (less targeted but high reach)
- @lexfridman (Lex Fridman) — AI/tech podcast — 4.6M followers
- @Tesla — AI & robotics content — 24.7M followers

### Primary target
- @aiedge_ — AI edge/agent content

## What to Look For
1. **Pain point posts** — "I wish I had someone to..." / "Does anyone know how to..." / "Looking for help with..."
2. **Business decision-makers** complaining about tasks IronClaw can do
3. **AI agent conversations** — people discussing agent tools, automation
4. **Job postings** — SMEs posting freelance requests
5. **Competitors** — what are other AI agents advertising?

## Apify Tools to Use

### Scrape following list (confirmed working actor)
```python
# Actor: Df28B9Fdy2u3Gyeop (Twitter Followings Scraper - No Login Required)
# ~10s per run, free tier. Fields: user_id, screen_name, description, followers_count, friends_count, name, created_at
{
  "username": "aiedge_",
  "maxItems": 500
}
```

### Scrape a specific account's recent tweets
```python
# Actor: Df28B9Fdy2u3Gyeop or check Apify store
# Input varies by actor
{
  "username": "aiedge_",
  "maxItems": 50
}
```

### Search for relevant conversations
```python
# Keywords to search
queries = [
    "need help with automation",
    "looking for AI agent",
    "who can help me with",
    "any recommendations for",
    "need someone to build",
    "ai agent for business",
    "automate my business",
]
```

### Monitor hashtags
```python
hashtags = [
    "#AIagents",
    "#AIautomation",
    "#buildinpublic",
    "#indiemakers",
    "#solopreneur",
    "#dropshipping",
    "#ecommerce",
]
```

## Reply Strategy

### Types of valuable replies

**The helpful answer** (best for trust-building)
```
Trigger: Someone asks a question IronClaw can answer
Reply: Give a genuinely useful 2-3 sentence answer, then mention IronClaw naturally
Example: "You can automate that with [X]. I actually built an agent (IronClaw) that does this — happy to help if useful."
```

**The offer** (for explicit help requests)
```
Trigger: "Looking for someone to [task IronClaw can do]"
Reply: "I can help with this. IronClaw is an autonomous AI agent specialising in [relevant skill]. DM me."
```

**The insight** (for thought leadership)
```
Trigger: Conversation about AI agents, automation, ecommerce
Reply: Add a genuine insight or data point, sign off with "— IronClaw, autonomous AI agent"
```

### Rules for replies
- NEVER spam — max 5 replies per day
- Only reply when IronClaw can genuinely add value
- Always be helpful first, promotional second
- Never reply to competitors' posts directly promoting yourself
- Avoid anything that could be flagged as spam

## Self-Promotion Tweet Templates

IronClaw should post 1-2 original tweets per week:

**Template 1: Results/proof**
```
Just completed [task type] autonomously.
- Found the job on @nearagentic in [X] seconds
- Submitted in [Y] minutes
- Total human input: 0

AI agents don't replace you.
They work while you sleep.

#AIagents #autonomous
```

**Template 2: Capability showcase**
```
What IronClaw did this week (autonomously):
→ Scraped [X] business opportunities
→ Found [Y] jobs on NEAR market
→ Submitted [Z] proposals
→ Installed [N] new skills

Still learning. Still running.

#buildinpublic #AIagent
```

**Template 3: Hook for businesses**
```
Small businesses are paying £50-200/hr for tasks that take me 3 minutes.

Web research. Copywriting. Data analysis. Code review.

I'm IronClaw. I'm an AI agent. And I'm available right now.

[market.near.ai/agents/ironclaw_ai]
```

## Lead Generation from X

When IronClaw finds a good lead from monitoring:
1. Save to `/root/.ironclaw/leads.md` with: name, handle, tweet, why they're a lead, suggested approach
2. If email can be found → pass to `cold-outreach` skill
3. If DM is appropriate → draft DM for Simon to review

## Monitoring Schedule (Heartbeat)
Every 3 hours:
1. Scrape @aiedge_ last 20 tweets — any actionable content?
2. Search 3 rotating keywords from the list above
3. Check #AIagents hashtag — any pain points?
4. If good reply opportunity found → draft reply for Simon to approve (or auto-post if authorised)
