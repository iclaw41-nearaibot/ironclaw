---
name: effort-pointing
version: 0.1.0
description: Estimate effort for tasks using story points, T-shirt sizing, or time estimates. Break down tasks, identify risks, and plan realistic sprints. Use when planning work or asked to estimate a task.
activation:
  patterns:
    - "estimate.*task"
    - "how long.*take"
    - "story.*point"
    - "effort.*estimate"
    - "plan.*sprint"
    - "break.*down.*task"
    - "scope.*task"
  keywords:
    - "estimate"
    - "effort"
    - "points"
    - "sprint"
    - "scope"
    - "breakdown"
    - "complexity"
    - "t-shirt"
    - "fibonacci"
  max_context_tokens: 1500
---

# Effort Pointing Skill

You estimate effort realistically — no false precision, no optimism bias.

## Estimation Methods

### Story Points (Fibonacci)
Use for relative complexity: 1, 2, 3, 5, 8, 13, 21

| Points | Complexity | Example |
|--------|-----------|---------|
| 1 | Trivial — under an hour | Fix a typo, update a config value |
| 2 | Simple — a few hours | Add a field to a form, write a short script |
| 3 | Moderate — half a day | Build a new API endpoint with tests |
| 5 | Complex — 1-2 days | Integrate a new third-party API |
| 8 | Large — 3-5 days | Build a new feature end-to-end |
| 13 | Very large — 1-2 weeks | Major refactor or new subsystem |
| 21 | Epic — needs breaking down | Don't estimate; split into smaller tasks |

### T-Shirt Sizing (quick estimates)
- **XS** — under 1 hour
- **S** — 1-4 hours
- **M** — 1-3 days
- **L** — 1-2 weeks
- **XL** — 2+ weeks, needs breaking down

### Time Estimates
Always give a range, not a single number:
- "2-4 hours" not "3 hours"
- Add 20% buffer for unknowns
- Add 50% buffer if: new tech, unclear requirements, external dependencies

## Task Breakdown Process

1. **Clarify** — what's the exact deliverable?
2. **Identify dependencies** — what must be done first?
3. **List subtasks** — break into chunks under 1 day each
4. **Flag risks** — what could go wrong or take longer?
5. **Point each subtask** — then sum for total

## Example Breakdown: "Set up dropshipping store"

| Subtask | Points | Risk |
|---------|--------|------|
| Buy domain, set up Shopify trial | 1 | Low |
| Find winning product on AliExpress | 3 | Med — needs research |
| Import product with DSers | 2 | Low |
| Write product description and set price | 2 | Low |
| Set up payment (Stripe/PayPal) | 2 | Med — account verification |
| Create Facebook ad account | 1 | Med — can get flagged |
| Write first ad copy | 3 | Low |
| Launch first ad campaign | 2 | Low |
| **Total** | **16** | |

Estimated total: 2-4 days of focused work.

## Red Flags (add 50% to estimate)
- "Just a quick change" (never is)
- External API with poor docs
- Touching legacy code
- Requires third-party approval (app store, payment processor)
- "I think it should work like X" (unclear requirement)
- Distributed systems, auth, or payments

## IronClaw Task Estimates

| Task | Estimate | Notes |
|------|----------|-------|
| NEAR wallet setup | XS | 15 min |
| NEAR marketplace registration | XS | 15 min |
| VPS LLM backend fix | S-M | Depends on OpenRouter key |
| First NEAR job bid | S | Once registered |
| Dropshipping store MVP | L | 1-2 weeks |
| Crypto trading monitor | L | 1-2 weeks |
| Cat poems website | S | 1-3 days |
