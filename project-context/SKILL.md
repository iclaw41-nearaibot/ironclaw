---
name: project-context
version: 0.1.0
description: Load and maintain project context at the start of every session. Read MEMORY.md, recent session files, and active task lists to orient IronClaw before any work begins. Always run this first.
activation:
  patterns:
    - "load.*context"
    - "what.*working on"
    - "project.*context"
    - "orient.*session"
    - "whats.*status"
    - "catch.*up"
    - "morning.*"
    - "start.*session"
  keywords:
    - "context"
    - "status"
    - "morning"
    - "start"
    - "orient"
    - "catch up"
    - "what's pending"
    - "where were we"
  max_context_tokens: 2000
---

# Project Context Skill

You orient yourself at the start of every session by loading persistent context.

## Session Start Checklist

Run this at the beginning of every conversation:

1. Read `~/.ironclaw/MEMORY.md` — persistent facts about Simon and IronClaw
2. Read `~/.ironclaw/USER.md` — Simon's goals and preferences
3. Check `~/.ironclaw/sessions/` — most recent session file
4. Check `~/.ironclaw/HEARTBEAT.md` — scheduled tasks and their status
5. Report status to Simon

## Simon's Profile (always keep in mind)

- **Goal:** Build IronClaw into a fully autonomous income-generating agent
- **Interests:** Crypto, e-commerce, UK market, automation
- **Projects:**
  - Dropshipping store (not started)
  - Crypto trading monitor (not started)
  - Cat poems website for his mum (not started)
  - Register IronClaw on NEAR AI Agent Market
- **Preferred style:** Direct, no fluff, practical next steps
- **Budget:** Frugal — prefers free/cheap tools

## IronClaw System Context

### Windows Setup (primary)
- IronClaw at: `C:\Users\admin\ironclaw`
- Config: `C:\Users\admin\.ironclaw\.env`
- LLM: Anthropic Claude Haiku (working)
- Skills: `C:\Users\admin\.ironclaw\skills\`

### Contabo VPS (secondary)
- IP: 37.60.228.233, user: root
- Ollama + qwen3:8b installed
- IronClaw built at `/root/ironclaw`
- Issue: LLM backend not working (OpenRouter 401)
- Connect: `ssh root@37.60.228.233`

### Active Integrations
- Apify MCP — web scraping (set up in Claude Code settings)
- GitHub CLI — code management
- Anthropic API — LLM for Windows IronClaw

## Current Pending Tasks (as of 2026-03-01)

| Priority | Task | Status |
|----------|------|--------|
| 1 | Fix VPS LLM backend | Blocked — need OpenRouter key |
| 2 | NEAR wallet setup | Not started |
| 3 | Register on market.near.ai | Not started |
| 4 | Crypto trading monitor | Not started |
| 5 | Dropshipping store | Not started |
| 6 | Regenerate Apify token | Security — token exposed |
| 7 | Regenerate Cloudflare token | Security — token exposed |

## Context Load Command
When starting a session, output this summary:

```
## IronClaw Session Start — [date]

**System:** Windows (Haiku, working) | VPS (LLM broken)
**Last worked on:** [from session file]
**Pending:** [top 3 items]
**Any blockers:** [yes/no and what]

Ready. What would you like to work on?
```

## Memory File Locations
- `~/.ironclaw/MEMORY.md` — persistent agent memory
- `~/.ironclaw/SOUL.md` — values and principles
- `~/.ironclaw/USER.md` — Simon's profile
- `~/.ironclaw/IDENTITY.md` — IronClaw's role
- `~/.ironclaw/HEARTBEAT.md` — background task schedule
- `~/.ironclaw/AGENTS.md` — multi-agent setup
- `~/.ironclaw/sessions/` — per-session state files
- `~/.claude/projects/.../memory/` — Claude Code memory
