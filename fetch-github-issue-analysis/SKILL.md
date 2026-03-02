---
name: fetch-github-issue-analysis
version: 0.1.0
description: Fetch and analyse GitHub issues for a repository. Identify patterns, common bugs, feature gaps, popular requests, and competitor weaknesses. Use for market research, support analysis, or competitive intelligence.
activation:
  patterns:
    - "analyse.*issues"
    - "github.*issues.*analysis"
    - "what.*people.*complaining"
    - "common.*bugs.*"
    - "competitor.*issues"
    - "feature.*gaps"
    - "issue.*patterns"
  keywords:
    - "issue analysis"
    - "github issues"
    - "bug patterns"
    - "feature gaps"
    - "competitor weakness"
    - "support analysis"
    - "pain points"
  max_context_tokens: 2000
---

# Fetch GitHub Issue Analysis Skill

You analyse GitHub issue trackers to find patterns, pain points, and business opportunities.

## Use Cases
1. **Competitor weakness research** — find what users hate about a competitor's product
2. **Feature gap analysis** — find what features users keep requesting
3. **Support pattern analysis** — find recurring bugs consuming support time
4. **Product research** — understand real user pain before building

## Analysis Process

### Step 1: Fetch Issues
Use GitHub CLI or GitHub MCP:
```bash
# Get open issues with labels, sorted by reactions
gh issue list --repo owner/repo --state open --limit 100 --json title,body,labels,comments,reactions,createdAt

# Get most-reacted issues (popular pain points)
gh issue list --repo owner/repo --state open --limit 100 --json title,reactions | \
  python3 -c "import json,sys; data=json.load(sys.stdin); sorted_data=sorted(data, key=lambda x: x['reactions']['total_count'], reverse=True); [print(f\"{d['reactions']['total_count']:4d} 👍  {d['title']}\") for d in sorted_data[:20]]"

# Get closed issues (bugs that were real)
gh issue list --repo owner/repo --state closed --label bug --limit 100 --json title,closedAt
```

### Step 2: Categorise Issues
Group issues into buckets:
- **Bugs** — broken functionality
- **Feature requests** — missing functionality
- **Performance** — too slow, memory issues
- **Documentation** — unclear, missing docs
- **Installation/Setup** — onboarding friction
- **Integration** — doesn't work with X

### Step 3: Score by Impact
For each category, count:
- Number of issues
- Total reactions (upvotes)
- Comment count (engagement = real pain)
- Recency (old issues may be fixed)

### Step 4: Identify Patterns

Look for:
- **Recurring errors** — same error message appearing repeatedly
- **Missing integrations** — "does it work with X?" appearing often
- **Onboarding failures** — issues from users < 1 week old
- **Version regression** — issues saying "worked in vX.X"
- **Competitor mentions** — "unlike X, this doesn't..."

### Step 5: Opportunity Report

```markdown
## GitHub Issue Analysis: [Repo Name]
Date: [date]
Issues analysed: [n]

### Top Pain Points
1. **[Category]** — [n] issues, [n] total reactions
   - Example: "Error when connecting to PostgreSQL on Windows"
   - Opportunity: [What could be built/fixed/offered]

2. **[Category]** — [n] issues, [n] total reactions
   ...

### Feature Gaps (Most Requested)
1. [Feature] — [n] requests, [n] reactions
2. [Feature] — [n] requests

### Competitive Opportunity
Users frequently mention wanting [X]. No existing solution does this well.
→ Opportunity: Build [X] as a competing product or plugin.

### Recommended Action
[Specific next step based on analysis]
```

## Quick Commands

### Find most painful issues in any repo
```bash
gh issue list --repo vercel/next.js --state open --limit 200 \
  --json title,reactions,comments \
  --jq 'sort_by(-.reactions.total_count) | .[:10] | .[] | "\(.reactions.total_count) 👍 \(.title)"'
```

### Find all feature requests
```bash
gh issue list --repo owner/repo --label "feature request" --state open \
  --json title,reactions --jq 'sort_by(-.reactions.total_count) | .[:20][]  | "\(.reactions.total_count) | \(.title)"'
```

### Count issues by label
```bash
gh issue list --repo owner/repo --state open --limit 500 \
  --json labels --jq '[.[].labels[].name] | group_by(.) | map({label: .[0], count: length}) | sort_by(-.count) | .[:15][]'
```

## IronClaw Applications
- Analyse competitor dropshipping tools → find feature gaps to exploit
- Analyse Shopify app issues → find underserved niches
- Analyse crypto bot repos → find what traders want but can't get
- Track issues in repos Simon contributes to → NEAR market opportunities
