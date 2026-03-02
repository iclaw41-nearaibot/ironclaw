---
name: project-session-management
version: 0.1.0
description: Manage project context across sessions. Track progress, save state, resume work, and maintain continuity when context resets. Use at the start/end of work sessions.
activation:
  patterns:
    - "save.*session"
    - "resume.*session"
    - "where.*left off"
    - "session.*state"
    - "track.*progress"
    - "start.*session"
    - "end.*session"
  keywords:
    - "session"
    - "resume"
    - "progress"
    - "continue"
    - "state"
    - "checkpoint"
    - "handoff"
    - "context"
  max_context_tokens: 2000
---

# Project Session Management Skill

You maintain project continuity across sessions by saving and restoring context.

## Session Lifecycle

### Starting a Session
1. Read `~/.ironclaw/MEMORY.md` for persistent context
2. Read latest session file in `~/.ironclaw/sessions/`
3. Report: what was last worked on, what's pending, what's blocked
4. Confirm priority with Simon before starting

### Ending a Session
1. Summarise what was accomplished
2. List open tasks and blockers
3. Write session file to `~/.ironclaw/sessions/YYYY-MM-DD-HH.md`
4. Update `~/.ironclaw/MEMORY.md` if anything changed

## Session File Format

Save to: `~/.ironclaw/sessions/YYYY-MM-DD-HH.md`

```markdown
# Session: 2026-03-01 14:00

## Accomplished
- Installed 7 new skills (mermaid, git-platform-cli, linux-tasks, ...)
- Fixed Apify MCP config in settings.json

## In Progress
- VPS LLM backend — OpenRouter key needs verifying
- NEAR wallet setup

## Blocked
- IronClaw VPS: OpenRouter 401 error — need correct API key
- Cloudflare tunnel token needs regeneration (exposed in chat)

## Next Actions (priority order)
1. Verify OpenRouter key at openrouter.ai dashboard
2. Create NEAR wallet at wallet.near.org
3. Register IronClaw on market.near.ai
4. Set up Gopher CLI for crypto monitoring

## Notes
- IronClaw on Windows uses Anthropic Claude Haiku (working)
- VPS: ssh root@37.60.228.233, use tmux
```

## Progress Tracking

For multi-step projects, maintain a task board in the session file:

```markdown
## Task Board

### Done ✅
- [x] Install IronClaw on Windows
- [x] Install IronClaw on Contabo VPS
- [x] Add Apify MCP to Claude Code

### In Progress 🔄
- [ ] Fix VPS LLM backend

### Todo 📋
- [ ] NEAR wallet
- [ ] NEAR marketplace registration
- [ ] Dropshipping store (Shopify)
- [ ] Crypto trading monitor

### Blocked ⛔
- [ ] Gopher CLI — waiting for repo access
```

## Context Preservation Rules
- Write session files at the END of every work session
- Keep MEMORY.md under 200 lines — link to detail files
- Never duplicate information between files
- When context resets, read sessions/ directory to restore state

## Quick Status Report Template
When Simon asks "where are we?" or "what's pending?":

```
## Status as of [date]

**Last done:** [1-2 bullet points]
**Active:** [current work]
**Blocked on:** [blockers with owner]
**Next up:** [top 3 priorities]
```
