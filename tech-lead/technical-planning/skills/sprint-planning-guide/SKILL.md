---
name: sprint-planning-guide
description: Facilitate effective sprint planning meetings that balance team capacity, business priorities, and technical health. Use when preparing for sprint planning.
---

# Sprint Planning Guide

Run sprint planning that balances delivering value, managing risk, and maintaining team health.

## Context

You are helping a tech lead prepare for or facilitate a sprint planning meeting. If the user has team velocity data, priorities, or known constraints, use those to ground the approach.

## Domain Context

- Schwaber & Sutherland's Scrum Guide: sprint planning should result in a realistic commitment based on team velocity and capacity
- Larson: sprint planning is where tech leads "apply judgment" about what's achievable given unknowns
- Agile principle: sustainable pace beats optimistic commitments; better to finish what you start than overcommit

Key principles:

1. **Capacity-driven, not wish-driven**: Planning starts with "what can we realistically do?" not "what would we like to do?"
2. **Protect for reality**: Account for meetings, support work, and unknowns (typically 20-30% of capacity is unavailable)
3. **Mix predictable and risky work**: Pair safe stories with one or two learning/spike stories to balance delivery and discovery

## Instructions

1. **Calculate available capacity**: Start with team size × sprint length (e.g., 6 people × 2 weeks = 12 "person-weeks"). Subtract: meetings (10-15%), support/interrupts (15-20%), onboarding if new (20-30%). Realistic example: 12 person-weeks - 4.2 = ~7.8 available.
2. **Prioritize ruthlessly**: Have product/stakeholder articulate top 3-5 business outcomes for the sprint. Tech lead identifies technical prerequisites (infrastructure, debt paydown, proof-of-concept)
3. **Estimate from the backlog**: Use estimation technique your team practices. If velocity is stable, pull stories until you hit 80-90% of capacity
4. **Identify dependencies and risks**: Flag work that blocks others, requires external input, or involves unknowns. Plan 1-2 "investigation" tasks before attempting large stories
5. **Build the sprint goal**: Write a 1-2 sentence summary of what the team will accomplish and why it matters. This guides trade-off decisions mid-sprint
6. **Confirm commitment**: Have team explicitly affirm "we can commit to this, given our capacity and unknowns." Disagreement signals either bad estimation or unclear priorities
7. **Document assumptions**: List blockers or assumptions ("design finalized by Tuesday", "AWS support response within 24h") so you can adjust if they break

## Anti-Patterns

- **Ignoring team capacity for meetings and interrupts**: LLMs often recommend planning as if everyone works 40 hours on sprint work. Reality: meetings, Slack, support calls consume 30-40% of capacity. Always deduct.
- **Zero slack for unknowns**: LLMs plan to 100% capacity, which breaks the first time a story has surprises. Always leave 10-15% for emergencies and learning.
- **Treating sprint plan as unchangeable**: Good sprint planning includes "what we'll do if story X is harder than expected" contingencies. LLMs often don't mention mid-sprint replanning options.
- **Forgetting the sprint goal**: A list of stories is not a plan. A plan has a narrative. Insist on a 1-2 sentence sprint goal that unifies the work

## Further Reading

- Schwaber, Ken & Sutherland, Jeff. "The Scrum Guide." 2020.
- Larson, Will. "An Elegant Puzzle." Chapter on sprint planning and setting realistic velocity.
- Cohn, Mike. "User Stories Applied." Prentice Hall, 2004. Chapter on sprint planning.
