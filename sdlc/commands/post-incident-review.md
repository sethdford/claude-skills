---
description: Transform an incident into systemic improvements across all teams.
argument-hint: "[incident name or ID]"
---

Conduct a thorough incident review that transforms the incident into lasting improvements.

## Steps

1. **Engineer Postmortem** (`engineer:postmortem-analysis`)
   - Input: Incident timeline, resolution steps
   - Output: What happened, how it was resolved

2. **Security Root Cause** (`security:root-cause-analysis-security`)
   - Input: Incident details
   - Output: Security impact, data compromise assessment

3. **Incident to Improvement** (`sdlc:incident-to-improvement`)
   - Input: Postmortem + security assessment
   - Output: Improvement recommendations by role

4. **Tech Lead Process Improvement** (`tech-lead:process-improvement`)
   - Input: Improvements, team capacity
   - Output: Implementation plan, timeline

5. **PM Backlog Prioritization** (`product-manager:prioritize-backlog`)
   - Input: Improvement items
   - Output: Prioritized backlog with owners

## Output

**Post-Incident Review Report** containing:

- Incident narrative and timeline
- Root cause analysis
- Security impact assessment
- Improvement recommendations by role
- Prioritized backlog items with owners and timelines
- Sign-offs from engineer, QA, security, tech lead, PM

## Example
```

/sdlc:post-incident-review "Payment processing timeout"

→ Postmortem: Timeout occurred because external payment API changed response time
→ Security: No data compromise, but rate-limiting was not enforced
→ Improvements: - Add circuit breaker to payment service (engineer, 8 hours) - Rate-limit external API calls (engineer, 4 hours) - Add timeout alerting (tech lead, 2 hours) - Add chaos testing for external dependencies (QA, 16 hours)
→ Backlog: 4 items prioritized for next sprint

Output: Post-Incident Review
Incident: Payment processing timeout affecting 500 customers for 8 minutes
Root Cause: External API response time increased from 50ms to 2s; no circuit breaker
Security Impact: None
Improvements: [list with owners and effort]
Backlog Items: [created and prioritized]
Sign-offs: [engineer] [QA] [security] [tech lead] [PM]

```

## Next Steps

- "Backlog items created and ready for sprint planning."
- "Follow up in 1 month to verify improvements were implemented."