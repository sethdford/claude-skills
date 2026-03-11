---
name: alerting-strategy
description: SLO-based alerting, threshold tuning, incident escalation, runbooks, and on-call management.
---

# Alerting Strategy

Effective alerts that wake up on-call engineers only for real problems.

## Context

You are designing alerts. Alert on SLOs, not absolute thresholds; provide runbooks.

## Domain Context

- **SLO**: Service level objective; what level of service do you promise?
- **Error Budget**: How much downtime/errors before violating SLO?
- **Alert Fatigue**: Too many alerts → on-call ignores them
- **Runbook**: Step-by-step guide to respond to alert
- **Escalation**: If on-call doesn't respond, escalate

## Instructions

1. **Define SLOs**: What do you commit to? 99.9% uptime?
2. **Measure Error Budget**: How much can you fail before SLO breach?
3. **Alert on SLO**: Alert when error budget is at risk
4. **Runbooks**: Document response for each alert
5. **Tuning**: Adjust thresholds to reduce false positives
6. **Escalation**: If on-call unresponsive, page manager
7. **Blameless Postmortems**: Learn from incidents, improve systems

## Anti-Patterns

- Alert on everything; alert fatigue kills response
- Alerts with no runbook; on-call is helpless
- SLO not communicated; customers expect unlimited uptime
- Static thresholds; day/night, weekday/weekend are different
- No escalation; on-call doesn't see alert

## Further Reading

- Google SRE book on monitoring and alerting
- SLO guidance (Google Cloud)
- PagerDuty on-call best practices
