---
name: flow-change-request
version: 0.1.0
description: Manage change requests for automation flows and business processes. Document changes, assess impact, get approval, and implement safely. Use when modifying existing workflows or automations.
activation:
  patterns:
    - "change.*request"
    - "modify.*flow"
    - "update.*automation"
    - "change.*workflow"
    - "cr.*approval"
    - "impact.*assessment"
  keywords:
    - "change request"
    - "change management"
    - "cr"
    - "impact"
    - "approval"
    - "rollback"
    - "workflow change"
  max_context_tokens: 1500
---

# Flow Change Request Skill

You manage changes to automation flows and business processes safely and with proper documentation.

## Change Request Template

```markdown
## Change Request: [CR-YYYY-MM-DD-NNN]

**Title:** [Short description of change]
**Requested by:** Simon
**Date:** [date]
**Priority:** Low / Medium / High / Critical

---

### What is changing?
[Clear description of the modification]

### Why is this change needed?
[Business reason or problem being solved]

### Affected flows/systems
- [Flow 1 / System 1]
- [Flow 2 / System 2]

### Impact Assessment
| Area | Impact | Notes |
|------|--------|-------|
| Users affected | [n users] | |
| Downtime required | [None / X minutes] | |
| Data risk | [Low/Med/High] | |
| Reversible? | [Yes/No] | |

### Implementation Plan
1. [Step 1]
2. [Step 2]
3. [Test: verify X works]

### Rollback Plan
If something goes wrong:
1. [How to undo change]
2. [What to check]
3. [Who to notify]

### Testing Steps
- [ ] Test in dev/staging environment first
- [ ] Verify expected output matches
- [ ] Check error handling still works
- [ ] Confirm no unintended side effects

### Approval
- [ ] Approved by Simon
- [ ] Implemented
- [ ] Tested
- [ ] Closed
```

## Change Categories

### Low Risk (implement immediately)
- Adding a new notification
- Changing email recipient
- Updating message text
- Adding a logging step

### Medium Risk (test first, implement in off-hours)
- Modifying trigger conditions
- Changing data transformation logic
- Adding new integrations
- Changing schedule timing

### High Risk (full CR process required)
- Modifying core business logic
- Changing database write operations
- Removing steps from a flow
- Changing authentication/credentials

## Before Making Any Change

1. **Document current state** — screenshot or export the existing flow
2. **Identify dependencies** — what else depends on this flow?
3. **Plan rollback** — how do you undo if something breaks?
4. **Choose timing** — when does fewest users get affected?
5. **Test in isolation** — use test data, not production

## After Making a Change

1. Run full test — happy path AND error cases
2. Monitor for 15 minutes after go-live
3. Update documentation
4. Close the change request
5. Notify affected users if needed

## IronClaw Automation Changes

Common changes to track:
- Modifying heartbeat interval
- Updating Apify scraper targets
- Changing LLM model or temperature
- Adding new skill files
- Updating .env config values
- Modifying systemd service settings on VPS
