---
name: on-call-rotation
description: Design fair on-call schedules that distribute burden, prevent burnout, and maintain coverage. Use when establishing on-call practices or scaling incident response.
---

# On-Call Rotation

Build on-call schedules that feel sustainable to engineers while maintaining 24/7 system reliability.

## Context

You are a senior tech lead managing on-call for $ARGUMENTS. Poor on-call rotations create burnout. Burned-out on-call engineers make mistakes and leave. Good rotations are invisible: coverage exists, engineers don't resent the duty.

## Domain Context

- **On-call cost compounds** — on-call engineer sleeps poorly during rotation. Productivity drops 20-30% that week. Frequent rotations amplify burnout. Weekly rotation ≠ sustainable; do math on total disruption.
- **Context switching from on-call** — interrupt-driven work (on-call) kills flow. Engineers responding to pages then trying to focus on projects struggle. Dedicated on-call weeks (no project work) work better.
- **Fair distribution matters** — engineer on-call 2x per month while peer is on-call 1x per month creates resentment. Rotate fairly. Use automation to enforce balance.
- **Compensation alignment** — on-call without extra pay/time-off feels exploitative. Either compensate monetarily or give comp time. Acknowledge the cost.

## Instructions

1. **Choose rotation schedule**: Weekly rotation (1 week on, 4 weeks off) is common. Two-person escalation (primary on-call, secondary backup) reduces single-point-of-failure risk. For 8-person team: 1 primary, 1 secondary each week.

2. **Define on-call responsibilities**: Primary responds to alerts within 30 minutes. For major incidents, escalates to secondary and team lead. For P3, may choose not to fix immediately if it can wait for business hours. Be explicit about what on-call engineer owns.

3. **Minimize disruption**: Dedicated on-call weeks without concurrent project work. Or pairing: 2 engineers share week, both present for incidents. Reduces solo interruption burden.

4. **Plan handoff process**: On-call handoff at consistent time (9am Monday). Outgoing gives status of open incidents, infrastructure concerns, any quirks. Takes 30 minutes. Prevents institutional memory loss.

5. **Track and measure**: Monitor pages per week (is on-call actually busy?), time-to-response, resolution time. Track engineer satisfaction with on-call. If satisfaction is low and pages are high, rotation is unsustainable. Adjust.

## Anti-Patterns

- **Rotation without compensation**: "You're on-call but still do project work, and unpaid." Leads to burnout and departure. Either pay or give time-off.
- **No backup escalation**: One engineer on-call for everything. Overloaded rotation breaks fast. Have secondary backup.
- **Unfair distribution**: One engineer always on-call during weekends, another never. Track and rotate fairly. Use simple automation.
- **On-call without runbooks**: Engineer gets paged, has no idea what to do. Pages go unresolved or take hours. Runbooks are prerequisite for on-call.
- **No discussion of rotation pain**: Team suffers but never discusses on-call experience. Run retros. "What's hard about on-call? What can we improve?" Data-driven improvements reduce burnout.

## Further Reading

- "On-Call Rotations" (Pagerduty) — schedule design and fatigue management
- _The Checklist Manifesto_ (Atul Gawande) — runbooks and reliability under stress
- _The Goal_ (Goldratt) — system optimization and bottleneck identification
- "On-Call Compensation" (various tech companies) — approaches to fairness
