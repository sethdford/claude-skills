---
name: on-call-runbook
description: Runbook templates, escalation procedures, playbooks, and incident playbooks.
---

# On-Call Runbook

Step-by-step guides for on-call engineers to respond to incidents.

## Context

You are writing runbooks for on-call response. Clear steps; testable.

## Domain Context

- **SEV 1**: Critical; customers affected; immediate response
- **SEV 2**: Significant; degraded service; urgent response
- **SEV 3**: Minor; workaround exists; routine response
- **Runbook**: Step-by-step; no thinking needed in panic
- **Escalation**: When to call manager/team

## Instructions

1. **Identify Alert**: Which alert triggered? What does it mean?
2. **Severity**: Is this SEV 1/2/3? Escalate if unsure
3. **First Steps**: What to check immediately? Logs? Dashboards?
4. **Diagnosis**: Tree of decision points; what do you observe?
5. **Actions**: What to try? Rollback? Scale? Restart?
6. **Escalation**: If you're stuck after 5 minutes, escalate
7. **Communication**: Keep team informed; update status page

## Anti-Patterns

- Runbooks that assume expert knowledge; useless for new on-call
- No decision trees; "check logs" and hope
- Runbooks for problems that don't exist; they drift
- No escalation path; engineer panics at 3am
- Not tested; worst time to discover runbook is wrong is during incident

## Further Reading

- Google SRE book on runbooks
- Incident management playbooks (PagerDuty)
- Runbook templates (open source)
