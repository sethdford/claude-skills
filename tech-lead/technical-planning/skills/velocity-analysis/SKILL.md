---
name: velocity-analysis
description: Track and interpret sprint velocity to forecast capacity, identify bottlenecks, and improve planning accuracy. Use when analyzing team productivity trends.
---

# Velocity Analysis

Use historical velocity data to improve estimates, identify process bottlenecks, and forecast capacity.

## Context

You are helping a tech lead analyze sprint velocity data to improve planning. If the user has velocity metrics from recent sprints, use them to ground analysis.

## Domain Context

- Agile Metrics: velocity is a tool for planning, not performance management (XP and Scrum communities agree on this distinction)
- Larson: "velocity is a lagging indicator"; it reflects what you've done, not what you can do
- Vacanti's "ActionableAgile" argues cycle time is more useful than velocity for capacity planning

Key principles:

1. **Velocity is for planning, not judgment**: Never use velocity to shame a team. It's a tool to forecast work capacity
2. **Stability matters more than magnitude**: A team with 40-point velocity that varies by 5 points is more predictable than one with 50-point velocity that varies by 20
3. **Velocity changes signal process changes**: If velocity drops, something structural changed (new process, team composition, project type). Investigate before assuming underperformance

## Instructions

1. **Gather historical data**: Collect velocity (story points or items completed) from last 8-13 sprints. This sample size lets you see trends and variations
2. **Calculate average and standard deviation**: Example: 8 sprints of data: 38, 42, 40, 45, 39, 41, 43, 37 → average ~40, std dev ~2.6 (stable). This team forecasts reliably at 40 ± 3 points
3. **Chart the trend**: Plot velocity over time. Look for:
   - Gradual increase (team improving, stabilizing after new process)
   - Sharp drop (process change, team composition change, major incident) — investigate the cause
   - High variance (unpredictable; looks like different types of sprints have different velocity)
4. **Stratify by sprint type**: If some sprints have deploys, incidents, or training, separate them. Example:
   - Standard sprints: 40 ± 2 points
   - Deploy sprints: 32 ± 3 points (lower, because deploy consumes capacity)
   - Learning sprints: 35 ± 4 points (lower due to training/onboarding)
5. **Identify bottlenecks**: Velocity drop or plateau often signals a bottleneck. Ask:
   - Are code reviews taking longer (blocked on reviewer availability)?
   - Are tests taking longer (CI slow, test suite bloated)?
   - Is scope creeping (stories growing mid-sprint)?
6. **Forecast with confidence bands**: Don't say "we'll do 40 points next sprint." Say "we'll do 40 ± 5 points with 80% confidence." Use this in roadmaps
7. **Set realistic commitments**: Use average minus 1 std dev as the conservative estimate for sprint commitment. Use average + 0.5 std dev as the optimistic estimate for roadmap planning
8. **Measure impact of process changes**: When you make a change (new CI tool, different refinement process), measure velocity 3 sprints before/after to see if it helped or hurt

## Anti-Patterns

- **Extrapolating without understanding cause**: If velocity drops 20%, LLMs sometimes suggest "work harder" without investigating root cause. Always ask "what changed?" before interpreting velocity shifts.
- **Ignoring sprint type variation**: LLMs often recommend 40-point sprints without noting that deploy sprints run at 30 points. Use stratified analysis, not an average that mixes types.
- **Using velocity to manage people**: Velocity is not a performance metric. If you use it to judge individual engineers or blame a team, they'll game the system by inflating estimates. Use velocity only for planning
- **Assuming velocity trend is permanent**: Velocity trends reverse (team learns, new hire ramps up). Don't assume that a 5-sprint uptrend continues forever. Revise estimates as new data arrives.

## Further Reading

- Vacanti, Daniel. "ActionableAgile: Metrics for Predictability." O'Reilly, 2014. Chapters on cycle time and velocity.
- Cohn, Mike. "Agile Estimating and Planning." Prentice Hall, 2005. Chapter on velocity as a planning tool.
- Larson, Will. "An Elegant Puzzle." Chapter on metrics and measurement.
