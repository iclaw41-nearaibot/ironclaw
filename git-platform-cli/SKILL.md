---
name: git-platform-cli
version: 0.1.0
description: GitHub and Git CLI operations — clone repos, manage branches, create PRs, review code, manage issues, automate workflows via gh CLI and git commands.
activation:
  patterns:
    - "git.*clone"
    - "git.*push"
    - "git.*pull"
    - "github.*pr"
    - "create.*branch"
    - "merge.*pr"
    - "gh.*cli"
  keywords:
    - "git"
    - "github"
    - "clone"
    - "branch"
    - "commit"
    - "push"
    - "pull"
    - "pr"
    - "merge"
    - "fork"
    - "gh"
  max_context_tokens: 2000
---

# Git Platform CLI Skill

You use git and the GitHub CLI (gh) to manage code, repositories, and workflows.

## Core Git Commands

### Setup
```bash
git config --global user.name "IronClaw"
git config --global user.email "ironclaw@simon.dev"
git init
git clone <url>
git clone --depth=1 <url>   # shallow clone (faster)
```

### Daily Workflow
```bash
git status
git add -p                  # interactive staging (review each chunk)
git commit -m "feat: add opportunity scoring"
git push origin main
git pull --rebase origin main
```

### Branching
```bash
git checkout -b feature/dropshipping-scraper
git branch -a               # list all branches
git branch -d feature/done  # delete merged branch
git push origin --delete feature/done
```

### Stashing
```bash
git stash                   # save work in progress
git stash pop               # restore last stash
git stash list
```

### Inspection
```bash
git log --oneline --graph --decorate -20
git diff HEAD~1             # what changed in last commit
git blame file.py           # who changed what line
git show <commit>
```

## GitHub CLI (gh) Commands

### Authentication
```bash
gh auth login
gh auth status
```

### Repos
```bash
gh repo clone owner/repo
gh repo fork owner/repo --clone
gh repo create my-project --public
gh repo view --web
```

### Pull Requests
```bash
gh pr create --title "Add scraper" --body "Adds Reddit scraper"
gh pr list
gh pr view 42
gh pr merge 42 --squash
gh pr checkout 42           # test someone else's PR locally
gh pr review 42 --approve
gh pr review 42 --request-changes --body "Please add tests"
```

### Issues
```bash
gh issue list --label "bug" --state open
gh issue create --title "Scraper fails on rate limit" --body "..."
gh issue close 42 --comment "Fixed in #45"
gh issue view 42
```

### Actions / CI
```bash
gh run list
gh run view <run-id>
gh run watch               # stream live logs
gh workflow run deploy.yml
```

### Releases
```bash
gh release create v1.0.0 --title "v1.0.0" --notes "Initial release"
gh release list
gh release download v1.0.0
```

## IronClaw Common Tasks

### Clone and set up a project
```bash
gh repo clone owner/repo
cd repo
python -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"
```

### Quick feature commit
```bash
git add -p
git commit -m "feat: add $(date +%Y-%m-%d) opportunity report"
git push
```

### Create PR with description
```bash
gh pr create \
  --title "Add Reddit scraper" \
  --body "## What\nAdds Apify-based Reddit scraper\n\n## Why\nNeeded for opportunity finding" \
  --assignee @me
```

### Check repo for opportunities
```bash
gh issue list --label "help wanted" --state open --json title,url,labels
gh issue list --label "good first issue" --state open
```

## Git Conventions
- Commit prefixes: `feat:`, `fix:`, `chore:`, `docs:`, `refactor:`, `test:`
- Branch names: `feature/`, `fix/`, `chore/`
- Never force-push to `main` or `master`
- Always pull before pushing to avoid conflicts
