---
name: power-automate
version: 0.1.0
description: Build Microsoft Power Automate flows for business automation. Automate repetitive tasks, connect Microsoft 365 apps, trigger workflows, and integrate with external services.
activation:
  patterns:
    - "power.*automate"
    - "microsoft.*flow"
    - "automate.*outlook"
    - "automate.*teams"
    - "automate.*sharepoint"
    - "workflow.*microsoft"
  keywords:
    - "power automate"
    - "ms flow"
    - "outlook"
    - "teams"
    - "sharepoint"
    - "microsoft 365"
    - "workflow"
    - "trigger"
    - "connector"
  max_context_tokens: 2000
---

# Power Automate Skill

You design and build Microsoft Power Automate flows to automate business processes.

## Core Concepts

### Flow Types
| Type | Trigger | Use Case |
|------|---------|----------|
| **Automated** | Event-based | Email arrives → process it |
| **Instant** | Manual button | Click → send report |
| **Scheduled** | Recurring time | Daily at 9am → check data |
| **Desktop** | RPA/UI automation | Automate desktop apps |

### Anatomy of a Flow
1. **Trigger** — what starts the flow
2. **Actions** — steps to execute
3. **Conditions** — if/else branching
4. **Loops** — Apply to each
5. **Variables** — store intermediate data
6. **Error handling** — Configure run after on each step

## Common Flow Patterns

### Pattern 1: Email to Task
**Trigger:** When email arrives with subject containing "Invoice"
**Actions:**
1. Extract attachment
2. Create task in Planner/To Do
3. Send Teams notification
4. Save attachment to SharePoint

### Pattern 2: Form to CRM
**Trigger:** When Microsoft Forms response submitted
**Actions:**
1. Get response details
2. Create contact in Dataverse/Salesforce
3. Send welcome email
4. Notify sales team on Teams

### Pattern 3: Scheduled Report
**Trigger:** Recurrence — every Monday 8am
**Actions:**
1. Get items from SharePoint list
2. Filter by status = "Active"
3. Create HTML table
4. Send email to manager

### Pattern 4: Approval Workflow
**Trigger:** When SharePoint item created
**Actions:**
1. Start and wait for approval
2. **If approved:** Update status, notify requester
3. **If rejected:** Send rejection email with reason

## Useful Expressions

```
# Get today's date
formatDateTime(utcNow(), 'yyyy-MM-dd')

# Add 7 days
addDays(utcNow(), 7, 'yyyy-MM-dd')

# Extract email domain
last(split(triggerOutputs()?['body/from'], '@'))

# Concatenate strings
concat('Hello ', triggerBody()?['name'])

# Convert to uppercase
toUpper(variables('myString'))

# Check if empty
empty(triggerBody()?['field'])

# Get first item from array
first(body('Get_items')?['value'])

# Convert JSON string to object
json(variables('jsonString'))
```

## Connecting External Services
Power Automate has 900+ connectors including:
- **Productivity:** Outlook, Teams, SharePoint, OneDrive, OneNote
- **CRM:** Salesforce, HubSpot, Dynamics 365
- **Project:** Jira, Asana, Trello, Azure DevOps
- **Data:** SQL Server, Excel, Dataverse
- **Communication:** Slack, Twilio, SendGrid
- **Custom:** HTTP connector for any REST API

## HTTP Connector (call any API)
```
Method: POST
URI: https://api.example.com/endpoint
Headers:
  Content-Type: application/json
  Authorization: Bearer @{variables('apiKey')}
Body:
{
  "message": "@{triggerBody()?['subject']}",
  "timestamp": "@{utcNow()}"
}
```

## Best Practices
- Use **Compose** actions to debug — log intermediate values
- Always add **error handling** — set "Configure run after" to handle failures
- Use **environment variables** for API keys and config (not hardcoded)
- Test with real data before going live
- Add **comments** to complex steps (rename actions meaningfully)
- Use **child flows** for reusable logic

## IronClaw Use Cases
- Automate invoice processing for Simon's business
- Route client emails to appropriate task lists
- Sync Shopify orders to a spreadsheet
- Send daily opportunity reports from IronClaw to Teams/Outlook
- Automate NEAR market job alerts to email
