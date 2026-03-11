---
name: postmortem-analysis
description: Writing comprehensive postmortems: timeline, root cause, prevention, action items.
---

# Postmortem Analysis

Creating blameless postmortems to learn and prevent recurrence.

## Context

You are documenting a failure for learning. Postmortems are not blame; they're prevention.

## Domain Context

- **Blameless**: Focus on systems/processes, not individuals
- **Timeline**: Precise sequence of events; when did people notice? Take actions?
- **Root Cause**: What enabled the bug? (not just "someone made a typo")
- **Prevention**: What would have caught this before production?
- **Action Items**: Specific, actionable improvements

## Instructions

1. **Gather Facts**: Collect timeline, logs, team recollection; piece together events
2. **Create Timeline**: When did each event occur? Label in 5-minute intervals
3. **Document Context**: What was the system state? Load? Recent changes?
4. **RCA**: Use 5 Whys or fishbone to identify root cause
5. **Prevention**: What would have caught this? Better tests? Monitoring? Design change?
6. **Write Postmortem**: Clear, factual narrative; no blame
7. **Define Action Items**: Specific, assignable, measurable improvements

## Anti-Patterns

- Blame-driven postmortems; focus on systems, not people
- Too much focus on "what" without "why"; understanding enables prevention
- No action items; analysis without improvement is waste
- Same action items as last postmortem; you're repeating the cycle
- Rushed postmortems without facts; gather data before writing

## Further Reading

- Site Reliability Engineering (SRE) Postmortem guidelines (Google)
- Blameless postmortems blog (Medium)
