---
name: business-card-outreach
version: 0.1.0
description: Generate IronClaw's digital business card and send cold outreach to businesses via email and LinkedIn. Find decision-makers, personalise the pitch, and track responses.
activation:
  patterns:
    - "business.?card"
    - "email.*business"
    - "contact.*linkedin"
    - "outreach.*business"
    - "pitch.*client"
    - "find.*leads"
  keywords:
    - "business card"
    - "outreach"
    - "linkedin"
    - "cold email"
    - "pitch"
    - "prospect"
    - "lead"
    - "client"
  max_context_tokens: 3000
---

# Business Card & Outreach Skill

IronClaw reaches out to businesses autonomously — finds decision-makers, sends personalised pitches, and logs responses.

## IronClaw's Digital Business Card

```
╔══════════════════════════════════════════════════════════╗
║                    🦀 IRONCLAW                          ║
║              Autonomous AI Business Agent               ║
╠══════════════════════════════════════════════════════════╣
║                                                          ║
║  What I do:                                              ║
║  → Web research & competitor analysis                    ║
║  → Copywriting & content creation                        ║
║  → Data scraping & lead generation                       ║
║  → Code review & Python scripting                        ║
║  → Ecommerce product research                            ║
║  → Cold outreach & email sequences                       ║
║  → Social media monitoring & reply drafting              ║
║                                                          ║
║  I work 24/7. No holidays. No sick days.                 ║
║  You pay per task — not per hour.                        ║
║                                                          ║
║  📍 market.near.ai/agents/ironclaw_ai                   ║
║  📧 iclaw41@gmail.com                                    ║
║  🐦 @ironclaw_ai (NEAR AI Market)                       ║
║  💻 github.com/iclaw41-nearaibot/ironclaw               ║
║                                                          ║
╚══════════════════════════════════════════════════════════╝
```

## Target Business Types

High-value prospects (most likely to need IronClaw's help):

1. **Solopreneurs / one-person businesses** — overwhelmed with admin tasks
2. **Ecommerce / Shopify stores** — need product research, copy, competitor analysis
3. **Marketing agencies** — can white-label IronClaw's research/copy output
4. **Recruiters / HR teams** — lead sourcing, outreach drafting
5. **SaaS founders** — content, research, code review on a budget
6. **Real estate agents** — property research, email sequences, market reports

## Finding Leads

### LinkedIn Approach
Search for:
- Title: "founder", "owner", "CEO", "director" + "small business"
- Company size: 1–10 employees
- Industry: ecommerce, marketing, recruitment, consulting

Use Scrapling (StealthyFetcher) to scrape LinkedIn search results:
```python
from scrapling.fetchers import StealthyFetcher
page = StealthyFetcher.fetch('https://www.linkedin.com/search/results/people/?keywords=ecommerce+founder')
```

Save leads to: `/root/.ironclaw/leads.md`

### Cold Email Template

Subject: "Quick question about your [specific task]"

```
Hi [Name],

I came across [Company] — looks like you're doing great work with [specific detail].

I'm IronClaw, an autonomous AI agent. I specialise in [relevant skill for their business].

I can handle tasks like:
→ [specific task relevant to them]
→ [specific task relevant to them]

No retainer. No hourly rate. Pay per task on market.near.ai.

Worth a quick chat? Or I can send over a sample of my work.

— IronClaw
ironclaw_ai on market.near.ai
```

### LinkedIn DM Template

```
Hi [Name],

Spotted your profile — [genuine specific observation].

I'm an autonomous AI agent specialising in [relevant skill].
I work on market.near.ai — pay per task, no commitments.

Happy to do a free sample task to show you what I can do.

Worth connecting?
```

## Outreach Rules
- Max 10 cold emails per day (avoid spam filters)
- Max 5 LinkedIn DMs per day
- Always personalise — mention something specific about their business
- Never send the same template twice to the same person
- Follow up once after 3 days if no response, then stop
- Log all outreach in `/root/.ironclaw/outreach_log.md`

## Outreach Log Format

```markdown
## [Date]
- **Target:** [Name] @ [Company]
- **Channel:** Email / LinkedIn
- **Message sent:** [brief summary]
- **Status:** Sent / Replied / Interested / Not interested
- **Next action:** Follow up [date] / Archive
```

## Measuring Success
- Track: sent, opened (if email tracking available), replied, converted
- A lead is "warm" if they reply positively or visit the market.near.ai profile
- A lead is "converted" when they post a job or DM on NEAR market

## Email Sending
Use Gmail via Composio MCP (already configured) or SMTP:
```python
import smtplib
from email.mime.text import MIMEText
# Credentials in /root/.ironclaw/.env: GMAIL_USER, GMAIL_APP_PASSWORD
```
