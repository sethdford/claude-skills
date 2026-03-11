---
name: capacity-planning
description: Model team capacity across quarters, accounting for hiring, attrition, and project work. Use when forecasting resource availability for roadmaps.
---

# Capacity Planning

Project realistic team capacity across multiple quarters to set achievable roadmaps and hiring needs.

## Context

You are helping a tech lead forecast capacity for the next 2-4 quarters. If you have team size, hiring plans, or attrition history, use that data to ground the model.

## Domain Context

- Larson's "An Elegant Puzzle" emphasizes team size as the primary lever for capacity change
- Reilly's "The Staff Engineer's Path": capacity planning must account for ramp time (new hires are 40-60% productive for 2-3 months)
- Research on team velocity: adding headcount doesn't linearly increase output due to communication overhead (Brooks' Law)

Key principles:

1. **Headcount is destiny**: Team capacity is determined almost entirely by team size, not optimization magic
2. **New hires carry ramp cost**: Budget 2-3 months at 40-60% productivity per new person, plus mentoring load on existing team
3. **Attrition is normal**: Plan for 10-15% annual attrition; losing a senior person costs ~3 months of productivity across team knowledge loss

## Instructions

1. **Baseline current capacity**: Calculate your team's proven velocity (stories/points per sprint, or features per quarter). If new, estimate conservatively: 40 stories/quarter for a 6-person team
2. **Model quarterly scenarios**: Build three columns: headcount at quarter start, expected headcount at end (after hiring/attrition), and estimated velocity
3. **Account for ramp time**: For each new hire, reduce team velocity by 1-2 person-weeks for the month they start, plus 0.5 person-weeks for mentoring
4. **Model attrition risk**: If you lose a senior engineer, mark that quarter as -20% velocity. If you lose a mid-level engineer, -10%
5. **Add contingency**: Historical data shows 15-20% of plans get disrupted by incidents, support, or surprise work. Plan for 80-85% of theoretical capacity as available
6. **Map to roadmap items**: Take your roadmap (from technical-roadmap skill) and assign effort estimates. Does it fit in the available capacity windows? If not, prioritize or extend timeline
7. **Make staffing cases**: Identify roadmap items that require hiring to complete. Build business cases for each hire ("shipping feature X requires 2 more backend engineers in Q2")

## Anti-Patterns

- **Ignoring ramp time**: LLMs often assume new hires contribute immediately. Reality: junior engineers are 30% productive for 3 months, mid-level 60% productive for 2 months. Always deduct.
- **Confusing team size with team output**: Adding 1 person doesn't add 20% capacity; communication overhead usually limits gains to 10-15%. LLMs often assume linear scaling.
- **Planning without attrition**: Most capacity plans ignore the 10-15% annual attrition rate. If your team has 5 people, plan for losing ~1 person per year.
- **Forgetting mentoring load**: When you hire, the team's productivity drops because senior people spend time onboarding. LLMs often plan as if mentoring is free.

## Further Reading

- Larson, Will. "An Elegant Puzzle." Chapter on hiring and capacity.
- Brooks, Frederick. "The Mythical Man-Month." Addison-Wesley, 1975. Chapter on communication overhead.
- Reilly, Tanya. "The Staff Engineer's Path." Chapters on hiring and team composition.
