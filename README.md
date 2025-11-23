
# Setup Guide - For Stacklok Team

## Quick Setup (5 minutes)

### 1. Create New Customer Repository

```bash
# Using GitHub CLI
gh repo create stacklok/support-[customer-name] \
  --template stacklok/customer-support-template \
  --private \
  --description "Support repository for [Customer Name]"
```

Or click "Use this template" button on GitHub web interface.

### 2. Customize for Customer

Update these files:

**README.md:**
- [ ] Replace `[Customer Name]` with actual customer name
- [ ] Update `[Your dedicated channel name]` with Slack channel name  
- [ ] Add Account Manager name and email
- [ ] Update strategic review schedule if different

**FAQ.md:**
- [ ] Add any customer-specific FAQs
- [ ] Update contact information

**CODE_OF_CONDUCT.md:**
- [ ] Add specific escalation contact email
- [ ] Update date

### 3. Grant Access

**GitHub Repository:**
```bash
# Add customer team members (write access so they can create issues)
gh repo add-collaborator stacklok/support-[customer-name] user@customer.com

# Add support team (maintain or admin access)
gh repo add-collaborator stacklok/support-[customer-name] support-engineer@stacklok.com --permission admin
```

**Slack Channel:**
- Create dedicated private channel (for real-time collaboration)
- Add customer contacts
- Add support engineers
- Pin link to GitHub repo

### 4. Send Welcome Email

```
Subject: Welcome to Your Stacklok Support Repository

Hi [Customer Name],

We've set up your dedicated support repository at:
https://github.com/stacklok/support-[customer-name]

How to Get Support:
1. Create a GitHub issue using one of our templates
2. Select the appropriate severity level
3. Our team will respond based on SLA
4. For urgent/complex issues, we'll invite you to Slack for real-time collaboration

Quick Links:
📋 GitHub Repo: [link]
📖 Severity Levels: [link to SEVERITY_LEVELS.md]
💬 Slack Channel: [channel name] (for active issues only)
⏰ Support Hours: Mon-Fri, 6 AM - 6 PM Pacific

Questions? Create an issue or ask your Account Manager.

Best regards,
Stacklok Support Team
```

## Daily Operations

### Handling Support Requests

1. **Customer creates GitHub issue**
   - Issue arrives in your queue
   - Note the severity level
   - Acknowledge within SLA time

2. **For Severity 1 (immediate)**
   - Acknowledge in GitHub within 1 hour
   - Invite customer to Slack immediately
   - Start real-time troubleshooting in Slack
   - Update GitHub issue with findings

3. **For Severity 2 (may need Slack)**
   - Acknowledge in GitHub within 4 hours
   - Assess if real-time collaboration would help
   - If yes, invite to Slack
   - Continue in Slack if needed, update GitHub

4. **For Severity 3/4 (usually GitHub only)**
   - Acknowledge within SLA
   - Work through issue in GitHub comments
   - Resolve directly in GitHub
   - Only use Slack if truly needed

5. **Resolution**
   - Document solution in GitHub issue
   - Ask customer to verify
   - Close issue once confirmed

### When to Use Slack

**Use Slack for:**
- Severity 1 issues (always)
- Real-time debugging sessions
- Screen sharing or live troubleshooting
- Quick back-and-forth when GitHub comments would be too slow
- Immediate updates on critical issues

**Stay in GitHub for:**
- Severity 3/4 issues (unless customer requests otherwise)
- Issues that need detailed documentation
- Async communication works fine
- Tracking and long-term reference

**Golden Rule**: Always start in GitHub (for SLA tracking), move to Slack when speed matters.

### Severity Guidelines

**Severity 1** (1 hour response):
- Production completely down
- Total inability to provide service
- Notify team immediately

**Severity 2** (4 hours response):
- Can work but significantly degraded
- Productivity impacted
- Multiple users affected

**Severity 3** (1 business day):
- Minor issues with workarounds
- Configuration questions
- Non-critical problems

**Severity 4** (No SLA):
- Feature requests
- General questions
- Best practices advice

### GitHub Issue Management

**All support starts with GitHub issues** - this is critical for SLA tracking and measurement.

**Issue Labels:**
- Use labels to track status (`in-progress`, `waiting-on-customer`, `resolved`)
- Severity labels are set by customer in template
- Add component labels as needed (`core`, `ui`, `api`, etc.)

**Linking Slack Conversations:**
- When moving to Slack, add Slack permalink to GitHub issue
- Example: "Moving to Slack for real-time debugging: [slack link]"
- Summarize Slack findings back in GitHub

**Issue Lifecycle:**
1. Customer creates issue → Auto-labeled by template
2. Support acknowledges → Add `in-progress` label
3. If Slack needed → Note in GitHub, link to Slack
4. Working on fix → Keep GitHub updated with progress
5. Resolved → Add `resolved` label, ask for verification
6. Verified → Close issue

**Never:**
- ❌ Resolve issues only in Slack without GitHub update
- ❌ Let issues sit without status updates
- ❌ Close without customer confirmation

### Version Support Reminders

When new major version releases:
1. Notify customer in Slack
2. Remind about 2-month grace period
3. Add calendar reminder for grace period end
4. Follow up as needed

After grace period:
- Downgrade Sev 1/2 issues to Sev 3 for old versions
- Communicate clearly about upgrade need

## Support Team Tips

### Response Templates

**Acknowledging Severity 1 (GitHub comment):**
```
🚨 Acknowledged - Severity 1

We've received your production issue. I'm inviting you to your dedicated Slack channel right now for immediate, real-time resolution.

Slack channel: [#customer-support-slack-channel]

We'll keep this GitHub issue updated with our findings.
```

**Acknowledging Severity 2 (GitHub comment):**
```
✅ Acknowledged - Severity 2

We're investigating this issue now. [If moving to Slack:] Let's move to your Slack channel for faster troubleshooting. I'll invite you now.

I'll provide updates here in GitHub as we progress.
```

**Acknowledging Severity 3/4 (GitHub comment):**
```
✅ Acknowledged

Thanks for reporting this. We're looking into it and will update you here in GitHub with our findings.
```

**Requesting More Info (GitHub comment):**
```
To help diagnose this quickly, could you provide:
- [Specific item 1]
- [Specific item 2]  
- [Specific item 3]

Adding the `waiting-on-customer` label. Thanks!
```

**Resolution Confirmation (GitHub comment):**
```
✅ Resolution

[Explain what was done]

Can you verify this is working as expected on your end? Once confirmed, I'll close this issue.
```

**Inviting to Slack (GitHub comment + Slack message):**
```
GitHub: "Moving to Slack for real-time collaboration: [slack permalink]"

Slack: "@customer Hi! I've started looking at your issue [link to GitHub issue]. Let's troubleshoot this together."
```

### Best Practices

✅ **Do:**
- Acknowledge all GitHub issues within SLA times
- Use Slack for Severity 1 and when real-time help needed
- Keep GitHub issues updated (even when in Slack)
- Document solutions in GitHub for future reference
- Link to Slack conversations from GitHub
- Update FAQ with common issues
- Be proactive about potential issues

❌ **Don't:**
- Resolve issues only in Slack without updating GitHub
- Let Sev 1/2 issues sit without updates
- Skip GitHub and go straight to Slack
- Over-promise resolution times
- Forget to follow up
- Use Slack for everything (defeats the purpose of tracking)
- Close issues without customer confirmation

## Troubleshooting

### Customer can't access GitHub
- Verify invitation was sent and accepted
- Check collaborator permissions
- Re-send invitation if needed

### Slack responses slow
- Check if message was during support hours
- Verify support team has notifications enabled
- Escalate if SLA at risk

### Version support questions
- Check customer's current version
- Compare to supported versions
- Calculate grace period end date if recent release
- Document in GitHub if needed

## Quick Reference

**SLA Response Times:**
- Sev 1: 1 hour
- Sev 2: 4 hours
- Sev 3: 1 business day
- Sev 4: No SLA

**Support Hours:**
Monday - Friday, 6 AM - 6 PM Pacific (excluding U.S. holidays)

**Supported Versions:**
- Current major version
- Previous major version
- 2-month grace period for upgrades

---

**Questions about this process?** Ask in #support-internal
