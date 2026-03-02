---
name: jira-sync
version: 0.1.0
description: Sync tasks and issues with Jira. Create, update, and query Jira issues via API. Map GitHub issues to Jira, sync sprint progress, and manage backlogs. Use when working with Jira project management.
activation:
  patterns:
    - "jira.*"
    - "sync.*jira"
    - "create.*ticket"
    - "jira.*ticket"
    - "sprint.*planning"
    - "jira.*api"
  keywords:
    - "jira"
    - "ticket"
    - "sprint"
    - "backlog"
    - "epic"
    - "story"
    - "jql"
    - "atlassian"
  max_context_tokens: 2000
---

# Jira Sync Skill

You create, update, and query Jira issues via the Jira REST API.

## Authentication Setup
```bash
export JIRA_BASE_URL="https://your-domain.atlassian.net"
export JIRA_EMAIL="simon@example.com"
export JIRA_API_TOKEN="your-api-token"  # from id.atlassian.com/manage-profile/security
```

## Core API Calls

### Create an Issue
```python
import os, requests
from requests.auth import HTTPBasicAuth

auth = HTTPBasicAuth(os.environ["JIRA_EMAIL"], os.environ["JIRA_API_TOKEN"])
base_url = os.environ["JIRA_BASE_URL"]

def create_issue(project_key: str, summary: str, description: str, issue_type: str = "Task") -> dict:
    payload = {
        "fields": {
            "project": {"key": project_key},
            "summary": summary,
            "description": {
                "type": "doc",
                "version": 1,
                "content": [{"type": "paragraph", "content": [{"type": "text", "text": description}]}]
            },
            "issuetype": {"name": issue_type}
        }
    }
    response = requests.post(f"{base_url}/rest/api/3/issue", json=payload, auth=auth)
    response.raise_for_status()
    return response.json()

# Usage
issue = create_issue("IRON", "Set up NEAR wallet", "Create wallet at wallet.near.org")
print(f"Created: {issue['key']}")
```

### Query Issues (JQL)
```python
def search_issues(jql: str, max_results: int = 50) -> list[dict]:
    params = {"jql": jql, "maxResults": max_results, "fields": "summary,status,assignee,priority"}
    response = requests.get(f"{base_url}/rest/api/3/search", params=params, auth=auth)
    response.raise_for_status()
    return response.json()["issues"]

# Examples
open_bugs = search_issues('project = IRON AND issuetype = Bug AND status != Done')
my_tasks = search_issues('assignee = currentUser() AND sprint in openSprints()')
high_priority = search_issues('priority in (High, Critical) AND status = "In Progress"')
```

### Update an Issue
```python
def update_issue(issue_key: str, fields: dict) -> None:
    response = requests.put(
        f"{base_url}/rest/api/3/issue/{issue_key}",
        json={"fields": fields},
        auth=auth
    )
    response.raise_for_status()

# Change status
update_issue("IRON-42", {"status": {"name": "In Progress"}})

# Add labels
update_issue("IRON-42", {"labels": ["ironclaw", "vps"]})
```

### Transition (change status)
```python
def transition_issue(issue_key: str, transition_name: str) -> None:
    # Get available transitions
    transitions = requests.get(f"{base_url}/rest/api/3/issue/{issue_key}/transitions", auth=auth).json()
    transition_id = next(t["id"] for t in transitions["transitions"] if t["name"] == transition_name)
    requests.post(
        f"{base_url}/rest/api/3/issue/{issue_key}/transitions",
        json={"transition": {"id": transition_id}},
        auth=auth
    )

transition_issue("IRON-42", "Done")
```

## JQL Quick Reference
```
# Open issues in project
project = IRON AND status != Done

# Issues due this week
due <= endOfWeek() AND status != Done

# Unassigned bugs
issuetype = Bug AND assignee is EMPTY

# Created in last 7 days
created >= -7d

# By label
labels = ironclaw

# Text search
summary ~ "wallet" OR description ~ "wallet"

# Sprint
sprint in openSprints() AND project = IRON
```

## GitHub → Jira Sync Pattern
```python
import subprocess, json

def sync_github_to_jira(repo: str, project_key: str) -> None:
    """Sync open GitHub issues to Jira"""
    result = subprocess.run(
        ["gh", "issue", "list", "--repo", repo, "--state", "open", "--json", "title,body,labels,number"],
        capture_output=True, text=True
    )
    issues = json.loads(result.stdout)

    for issue in issues:
        labels = [l["name"] for l in issue["labels"]]
        issue_type = "Bug" if "bug" in labels else "Story"
        create_issue(
            project_key=project_key,
            summary=f"[GH-{issue['number']}] {issue['title']}",
            description=issue["body"] or "",
            issue_type=issue_type
        )
        print(f"Synced GitHub #{issue['number']}")
```

## IronClaw Project Structure
Suggested Jira project: **IRON**

| Epic | Stories |
|------|---------|
| VPS Setup | Fix LLM backend, systemd service, monitoring |
| NEAR Market | Wallet, registration, first job |
| Dropshipping | Store setup, product research, ads |
| Crypto Trading | Monitor setup, backtesting, live alerts |
