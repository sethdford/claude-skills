---
name: change-management
description: Design change control processes that prevent production surprises while avoiding process paralysis. Use when coordinating multiple team changes or managing infrastructure modifications.
---

# Change Management

Build change control that prevents chaotic deployments while remaining lightweight enough that teams use it.

## Context

You are a senior tech lead managing change control for $ARGUMENTS. No change process = surprises and finger-pointing. Overly rigid change process = ignored by teams shipping anyway. Good process is invisible, not felt as burden.

## Domain Context

- **Change windows vs continuous deployment** — if system is stable and well-monitored, continuous deployment is lower risk than one-big-bang-release. If system is fragile, staged changes with observation windows reduce risk.
- **Communication is primary defense** — most change surprises come from lack of coordination (two teams changed same system without knowing), not process failure.
- **Risk assessment drives process** — simple config change vs database schema change require different approval rigor. One-size-fits-all process is either too loose or too strict.
- **Post-change observation is insurance** — ship change, then monitor for issues for 1+ hours before considering it done. Many issues surface in first hour.

## Instructions

1. **Classify changes by risk**: Low-risk (config, documentation, comment changes) = ship immediately. Medium-risk (new dependencies, DB migrations, API changes) = code review, testing, staged rollout. High-risk (multi-team coordination, infrastructure) = RFC process, staged phases, explicit approval.

2. **Create change template**: For medium/high-risk changes, document: what's changing, why, who's involved, rollback plan, monitoring plan, communications. Takes 30 minutes, prevents hours of debugging.

3. **Define change windows**: Specify deployment times (business hours typically safer). Allow emergency/urgent changes outside windows with incident process. Don't make process so rigid that critical security fixes wait for Monday.

4. **Establish communication protocol**: Notify affected teams before deploying. Inform support team of user-visible changes. Post in #incidents if change causes problem so people know what changed. Communication is primary defense.

5. **Monitor after change**: First hour post-deployment, watch error rates, latency, customer reports. If bad metric changes, rollback immediately. Don't wait for morning analysis. Observation window is insurance.

## Anti-Patterns

- **No change process, chaos**: Multiple teams deploy simultaneously, one breaks the other's work. Surprising everyone. Change process is minimum viable coordination.
- **Excessive gatekeeping**: "All changes must be approved by 5 people and scheduled 2 weeks in advance." Teams bypass process to ship. Bureaucracy builds resentment. Match process rigor to risk.
- **High-process, low-follow-up**: Documenting change requirements but not monitoring post-deployment. Change breaks production, catch it in morning analysis. Monitoring is the point of process.
- **No emergency bypass**: Strict change control for zero-day security fix. Can't deploy until Thursday's change window. Security risk wins. Have expedited process for true emergencies.
- **Change log not visible**: Change tracking exists but nobody uses it. Next incident, can't remember what changed Friday. Make change log visible and accessible.

## Further Reading

- _The Phoenix Project_ (Gene Kim) — change management and deployment
- "Change Advisory Board" (ITIL) — formal change management process
- _Release It!_ (Michael Nygard) — deployment patterns and change management
- "Chaos Engineering" (Gremlin) — testing system resilience to changes
