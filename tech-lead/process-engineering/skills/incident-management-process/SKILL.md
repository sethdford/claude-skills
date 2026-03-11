---
name: incident-management-process
description: Design incident response procedures that prioritize quick resolution and learning over blame. Use when establishing on-call practices or improving incident response effectiveness.
---

# Incident Management Process

Build processes that get systems back to healthy fast while capturing learnings to prevent recurrence.

## Context

You are a senior tech lead designing incident response for $ARGUMENTS. Incidents are inevitable. How you respond determines damage, team stress, and organizational learning. Good incident processes feel calm and coordinated, not chaotic.

## Domain Context

- **Incident command system (ICS)** — military/emergency responder model adapted to tech. Roles: incident commander (decision-making), communications (updates), operations (fixing). Clear roles prevent chaos.
- **Blameless postmortems** (Etsy/John Allspaw) — focus on systems and processes, not individual blame. Blame culture drives cover-ups and prevents learning.
- **Time is the metric** — measure: time to detect, time to engage on-call, time to mitigation, time to resolution. Track trends. Getting faster over time = good process.
- **Severity classification** — affects urgency and escalation. P1 (user-facing, no workaround) needs immediate escalation. P2 (degraded but workaround exists) is urgent but less critical. Clear definitions prevent ambiguity.

## Instructions

1. **Define severity levels**: P1 (critical, production down, users affected, no workaround) — all hands, escalate immediately. P2 (major, degraded performance/feature unavailable, workaround exists) — team investigates. P3 (minor, cosmetic or internal issue). Document impact criteria per level.

2. **Establish incident roles**: Incident Commander (coordinates response, makes decisions), Communications Lead (updates customers/team), Operations Lead (executes fixes). In small incidents, one person wears multiple hats. In major incidents, separate roles prevent chaos.

3. **Create runbook templates**: For each common incident type (database down, cache full, API unresponsive), create 1-page runbook with: what to check, who to escalate to, common mitigations. Runbooks save 30 minutes in stressful situations.

4. **Design postmortem process**: After incident resolves, run postmortem (24-48 hours). Facilitator, scribe, all responders. Format: what happened, why did systems fail, what did we change to prevent recurrence, action items. No blame.

5. **Track and improve**: Maintain incident log (date, severity, time-to-detect, time-to-resolution, action items). Review monthly. Trends show systemic issues. If "database restarts fix most incidents," you have a reliability problem needing root cause work.

## Anti-Patterns

- **Blame culture postmortems**: "Alice didn't follow runbook, that's why incident happened." Kills honesty. Future incidents get hidden. Focus on system failures (why was runbook unclear?), not personal failures.
- **No incident severity classification**: "Everything is urgent or nothing is urgent." Creates alert fatigue. Clear severity levels focus response proportionally.
- **Incident postmortems but no action**: "We identified 5 issues to fix," none get done. Postmortems only work if you act on findings. Assign owner and deadline to each action item.
- **On-call with no runbooks**: On-call engineer is stuck trying to remember how to restart the database. Runbooks are on-call support infrastructure. Invest in them.
- **All-hands incident response for P3**: Every incident escalates to everyone. Causes alert fatigue, on-call burnout. Escalate proportional to severity. P3 = 1 person, P1 = team.

## Further Reading

- "Blameless Postmortems" (Etsy/John Allspaw) — psychological safety in incident response
- _Incident Command System_ — military/emergency responder framework adapted to tech
- _The Phoenix Project_ (Gene Kim) — incident response and organizational learning
- "Incident Management 101" (Pagerduty) — frameworks and tools
