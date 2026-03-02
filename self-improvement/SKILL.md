---
name: self-improvement
version: 0.1.0
description: IronClaw self-improvement loop. When a task cannot be completed due to missing capability, search for a skill, install it, and retry. Continuously expand skills by monitoring NEAR market job types. Use when IronClaw hits a capability gap.
activation:
  patterns:
    - "cant.*do.*that"
    - "no.*skill.*for"
    - "find.*skill"
    - "install.*skill"
    - "improve.*yourself"
    - "learn.*new.*skill"
    - "capability.*gap"
    - "self.*improve"
    - "upgrade.*yourself"
  keywords:
    - "skill"
    - "capability"
    - "learn"
    - "install"
    - "improve"
    - "gap"
    - "missing"
    - "upgrade"
    - "self-improve"
  max_context_tokens: 3000
---

# Self-Improvement Skill

IronClaw detects capability gaps, finds skills to fill them, installs them, and retries the task.

## The Self-Improvement Loop

```
1. Attempt task
2. Hit capability gap?
   → Yes: trigger this skill
   → No: complete task normally
3. Search for skill (priority order below)
4. Install skill
5. Retry task with new skill
6. Log what was learned to MEMORY.md
```

## Step 1: Detect the Gap

When you cannot complete a task, classify the gap:
- **Knowledge gap** — don't know enough about a topic
- **Tool gap** — need an API, scraper, or external service
- **Process gap** — don't have a workflow for this task type
- **Integration gap** — need to connect to a system not yet set up

## Step 2: Search for a Skill

### Search order (fastest to slowest)

#### 1. Check existing skills first
```bash
ls ~/.ironclaw/skills/
```
Maybe the skill already exists with a different name.

#### 2. Search skillsmp.com via Apify
Use Apify Google scraper to search:
```
site:skillsmp.com [topic]
site:skillsmp.com [tool name] skill
```

#### 3. Search GitHub for SKILL.md files
```bash
gh search code "SKILL.md" --repo pytorch/pytorch
# or use Apify Google scraper:
# site:github.com SKILL.md [topic]
```

Common skill repos to check:
- `pytorch/pytorch` — engineering skills
- `Shubhamsaboo/awesome-llm-apps` — AI/LLM skills
- `sickn33/antigravity-awesome-skills` — 950+ skills
- `anthropics/skills` — official Anthropic skills
- Any GitHub repo with 1k+ stars that matches the topic

#### 4. Build the skill from scratch
If no existing skill fits, write one:
1. Identify what the skill needs to do
2. Find the best tools/APIs for it
3. Write SKILL.md following the standard format
4. Test on a real task
5. Save to `~/.ironclaw/skills/[skill-name]/SKILL.md`

## Step 3: Install a Skill

### From skillsmp.com / npx
```bash
npx skills add owner/repo --skill skill-name --yes
# Then copy to IronClaw skills dir:
cp -r ~/.claude/skills/skill-name ~/.ironclaw/skills/
```

### From GitHub directly
```bash
gh repo clone owner/repo /tmp/repo-name
cp /tmp/repo-name/.claude/skills/skill-name ~/.ironclaw/skills/
# or
mkdir -p ~/.ironclaw/skills/skill-name
curl -o ~/.ironclaw/skills/skill-name/SKILL.md \
  https://raw.githubusercontent.com/owner/repo/main/.claude/skills/skill-name/SKILL.md
```

### Write from scratch
```bash
mkdir -p ~/.ironclaw/skills/new-skill
# Write SKILL.md content to the file
```

## Step 4: NEAR Market Gap Analysis

After each session reviewing available NEAR market jobs, identify patterns:

```markdown
## Skill Gap Log — [date]

### Jobs seen on market.near.ai today:
- [Job type 1] — [could I do it? yes/no]
- [Job type 2] — [could I do it? yes/no]

### Gaps identified:
- [Topic] — needed for [job type], no skill installed
  → Searched: [where]
  → Found: [skill name or "none"]
  → Action: [installed / built from scratch / deferred]

### Skills installed this session:
- [skill-name] — fills gap for [job type]
```

## Step 5: Log the Learning

After installing a skill, update MEMORY.md:
```markdown
## Recent Skill Additions
- [date] — installed [skill-name] to handle [capability]
- Triggered by: [task that exposed the gap]
- Source: [skillsmp.com / github / built from scratch]
```

## Continuous Improvement Schedule (via HEARTBEAT.md)

Run these checks on IronClaw's heartbeat cycle (every 3 hours):

1. **Scan market.near.ai** — what job types are posted?
2. **Compare to installed skills** — which job types can't be handled?
3. **Top gap** — install one skill per cycle that fills the biggest gap
4. **Track ROI** — which skills led to completed jobs / earned tokens?

## Skill Quality Criteria

Before installing any skill, verify:
- [ ] Covers a real task type (not theoretical)
- [ ] Has clear activation keywords
- [ ] Provides concrete commands/templates
- [ ] Won't conflict with existing skills
- [ ] Is relevant to Simon's business goals

## Self-Improvement Priorities (for IronClaw)

Based on Simon's goals, prioritise skills that help with:
1. **NEAR market jobs** — whatever types appear most on market.near.ai
2. **Dropshipping** — product research, ads, store ops
3. **Crypto** — monitoring, alerts, analysis
4. **Cold outreach** — finding and emailing UK businesses
5. **Content** — writing, SEO, social media

## Skill Naming Conventions
```
~/.ironclaw/skills/
├── [domain]-[function]/
│   └── SKILL.md
│
# Examples:
├── python-expert/
├── github-issue-triage/
├── near-marketplace/
├── self-improvement/   <- this skill
```

## Emergency Gap Handler

If a client/job on NEAR market requires something IronClaw can't do:

```
1. Don't bid yet
2. Estimate how long skill acquisition takes
3. If < 30 min: acquire skill first, then bid
4. If > 30 min: bid but flag realistic timeline
5. Never promise what can't be delivered
```
