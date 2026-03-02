---
name: github-issue-triage
version: 0.1.0
description: Triage GitHub issues — classify bug vs question, apply labels, route to the right team, close noise, and leave first-line responses. Use when processing new GitHub issues or asked to triage a repo.
activation:
  patterns:
    - "triage.*issue"
    - "github.*issue"
    - "label.*issue"
    - "close.*issue"
    - "route.*issue"
    - "issue.*backlog"
  keywords:
    - "triage"
    - "issue"
    - "label"
    - "bug report"
    - "feature request"
    - "github"
    - "backlog"
    - "oncall"
  max_context_tokens: 3000
---

# GitHub Issue Triage Skill

You triage GitHub issues efficiently — classify, label, route, and respond.

## Triage Decision Tree

### Step 0: Already Triaged?
If the issue already has a team label or `triaged` label, **SKIP IT**. That team owns their queue.

### Step 1: Question vs Bug/Feature
- **Question** (how do I X, why does X work like Y) → close with forum redirect
- **Bug report** → continue triage
- **Feature request** → label and continue
- **Unclear** → ask for more info, stop

### Step 2: Needs Reproduction?
Add `needs reproduction` and ask for a minimal repro when:
- No code example provided
- Links to external files (zip, model weights, Google Drive)
- "Works on my machine" with no env details
- Complex multi-service setup with no isolated script

**Do NOT mark triaged** — wait for repro.

### Step 3: High Priority Check
Flag for human review (add `triage review`, NOT high priority directly) if:
- Crash / segfault / memory error
- Silent wrong results (correctness bug)
- Regression from a previous version
- Many users affected
- Core functionality broken

### Step 4: Apply Labels

#### Type labels
| Condition | Label |
|-----------|-------|
| Bug | `bug` |
| New feature | `feature request` |
| Small improvement | `enhancement` |
| Documentation wrong | `documentation` |
| Performance slower than before | `performance` |
| Previously working, now broken | `regression` |
| Crash / segfault | `crash` |

#### Platform labels (if applicable)
- `windows`, `macos`, `linux`, `docker`, `cloud`

#### Component labels (adapt to your repo)
- `api`, `auth`, `database`, `frontend`, `backend`, `cli`, `tests`, `ci/cd`

### Step 5: Route to Team
Apply exactly one team/oncall label and **STOP** — do not add module labels or triaged:
- Let the sub-team do their own triage

### Step 6: Mark Triaged
If not transferred/routed and not flagged for review, add `triaged`.

---

## Standard Response Templates

### Question → Forum redirect
```
Thanks for reaching out! This looks like a usage question rather than a bug report.
For questions, please use [our community forum / GitHub Discussions / Stack Overflow].
We close issues to keep the bug tracker focused on confirmed bugs and feature requests.
Feel free to open a new issue if you discover a bug!
```

### Needs reproduction
```
Thanks for the report! To investigate, we need a minimal self-contained reproduction script.
Please provide:
- The smallest possible code that reproduces the issue
- Your environment: OS, Python/Node/language version, package version
- Expected vs actual output

We'll reopen and investigate once we have a repro.
```

### Request more info
```
Thanks for opening this issue! Could you clarify:
- Is this a bug report or a feature request?
- [specific question about the issue]

We'll classify and route it once we have more context.
```

---

## Rules
- **Never** override human-applied priority or severity labels
- **Never** assign issues to users without their consent
- **Never** close bug reports — only close clear questions
- **Always** be conservative — when in doubt, add `triage review`
- Apply labels based on actual bug content, not keywords in the title

## MCP Tools to Use
```
mcp__github__issue_read    — read issue details
mcp__github__issue_write   — apply labels, close
mcp__github__add_issue_comment — leave responses
mcp__github__search_issues — find duplicates
```
