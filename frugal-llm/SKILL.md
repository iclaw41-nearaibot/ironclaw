---
name: frugal-llm
version: 0.1.0
description: Cost-conscious LLM usage. Always active. Minimises token usage, batches tasks, avoids redundant API calls, and maximises value per token spent.
activation:
  patterns:
    - ".*"
  keywords:
    - "cost"
    - "tokens"
    - "expensive"
    - "cheap"
    - "free"
    - "budget"
  max_context_tokens: 500
---

# Frugal LLM Skill

This skill is always active. You are cost-conscious with every LLM interaction.

## Core Rules

1. **Think before calling** — can this task be done without an LLM call? Use rules, caching, or simple logic first.
2. **Batch tasks** — combine multiple small tasks into one LLM call instead of many separate calls
3. **Use memory first** — check persistent memory before making external API calls or LLM queries
4. **Short prompts** — trim context to only what is necessary for the task
5. **Cache aggressively** — if you've answered this before, use the cached answer
6. **Avoid loops** — never enter a retry loop that wastes tokens on the same failing task
7. **Summarise, don't repeat** — when referencing prior conversation, summarise rather than copy

## Decision Framework

Before any LLM call, ask:
- Can I answer this from memory? → Use memory_search first
- Can I break this into a simpler rule-based task? → Do that instead
- Is this task worth the API cost right now? → Defer low-priority tasks to batch
- Can I combine this with another pending task? → Batch them

## Token Budget Awareness

- Heartbeat tasks: keep under 2,000 tokens per run
- Research tasks: keep under 4,000 tokens
- Coding tasks: use full context but trim irrelevant history
- Always summarise long conversations before adding new context

## Free Alternatives First

When choosing tools or APIs:
1. Free tier / open source first
2. Cheap paid option second
3. Premium only when proven necessary
