---
name: estimation-techniques
description: Apply evidence-based estimation methods (story points, t-shirt sizing, planning poker) to reduce uncertainty. Use when sizing work for sprints or releases.
---

# Estimation Techniques

Master multiple estimation approaches and when to apply each to improve planning accuracy.

## Context

You are helping a tech lead and team establish or improve estimation practices. If the user provides historical velocity data or team composition, use it to ground recommendations.

## Domain Context

- #NoEstimates advocates (Allen Ward, Daniel Vacanti) argue cycle time and throughput matter more than estimates
- Agile community consensus: estimation is about communicating risk and driving conversation, not prediction
- Evidence from Larson and Fournier: teams that practice estimation develop better intuition about unknowns and dependencies

Key principles:

1. **Estimation reveals uncertainty, not destiny**: The goal is to surface what the team doesn't know
2. **Compare estimates to actuals**: Build feedback loops so the team learns its own accuracy patterns
3. **Right-size the effort**: Different estimation techniques fit different horizons (sprints vs. quarters)

## Instructions

1. **Choose the horizon**: Short-term (sprint) uses story points; medium-term (3 months) uses t-shirt sizing; long-term (roadmap) uses epic sizing with confidence bands
2. **For story points**: Have team rate relative effort (small, medium, large) against baseline stories. Use Fibonacci (1, 2, 3, 5, 8, 13) to force bucketing
3. **For t-shirt sizes**: Define S/M/L/XL in terms of days or weeks of effort, plus confidence. "M with 80% confidence" is better than "2 weeks"
4. **For planning poker**: In real-time estimation, discuss outliers (largest and smallest estimates) to surface hidden risks and assumptions
5. **Build a team estimate profile**: Track your team's estimates vs. actuals over 2-3 sprints to calibrate, then share with stakeholders
6. **Account for unknowns**: Always add a "spike" or investigation task if the team says "we don't know what we don't know"
7. **Decompose aggressively**: If anything is >13 points or >XL, it's probably not understood yet. Break it down

## Anti-Patterns

- **Treating estimates as commitments**: LLMs often present estimates as hard deadlines, not uncertainty ranges. Always say "we estimate 2-3 weeks with 70% confidence, but will know more after the design phase."
- **Skipping the "why" in estimation**: Teams can assign points without explaining what unknowns exist. Estimates without risk commentary are useless. Always ask "what could make this larger?"
- **Ignoring velocity variation**: LLMs assume linear velocity, but sprints with deploys, incidents, or learning are different. Account for sprint types (standard, deploy, learning) and show historical variance.
- **Estimation without feedback loops**: If you don't track actuals vs. estimates, the practice becomes cargo cult. Insist on retrospective calibration every sprint.

## Further Reading

- Larson, Will. "An Elegant Puzzle." Chapter on planning, velocity, and confidence bands.
- Vacanti, Daniel. "ActionableAgile: Metrics for Predictability." O'Reilly, 2014.
- Ward, Allen. "Lean Product and Process Development." Lean Enterprise Institute, 2007.
- Cohn, Mike. "Agile Estimating and Planning." Prentice Hall, 2005.
