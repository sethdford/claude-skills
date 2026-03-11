---
name: trade-off-analysis
description: Analyze architectural trade-offs systematically using decision matrices. Use when comparing design options or justifying architectural choices to stakeholders.
---

# Trade-Off Analysis

Systematically analyze and justify architectural decisions by explicitly modeling trade-offs across quality attributes.

## Context

You are comparing design options. The user faces conflicting requirements or needs to justify a choice. Read their constraints and objectives.

## Domain Context

Based on architectural decision-making frameworks and decision science:

- **Pareto Optimality**: No choice is best in all dimensions; understand which trade-offs matter
- **Decision Matrix**: Explicit scoring of options across criteria (cost, performance, maintainability, risk)
- **Quality Attributes**: Scalability, reliability, security, maintainability, cost, deployability
- **Stakeholder Alignment**: Different stakeholders weight quality attributes differently
- **Risk vs Reward**: Sometimes higher cost is justified by lower risk

## Instructions

1. **List Options**: Define 3-4 architectural choices to compare. Example: monolith vs microservices vs modular monolith.

2. **Define Evaluation Criteria**: List quality attributes that matter (scalability, cost, deployability, security). Weight by business importance.

3. **Score Each Option**: For each option, score (1-5) on each criterion. Be explicit about scoring rationale.

4. **Calculate Weighted Scores**: Multiply score by weight for each criterion. Sum for total. Option with highest score wins.

5. **Qualitative Analysis**: Beyond scores, document: risk factors, unknowns, conditions where another option would be better, reversibility.

## Anti-Patterns

- **Invisible Trade-Offs**: Choose option without explaining what's sacrificed. Result: stakeholders feel misled. **Guard**: Make trade-offs explicit; document what you're trading.
- **Wrong Weights**: Marketing says "fast deployment" matters; you weight reliability 90%. Result: chosen option disappoints. **Guard**: Align weights with stakeholder priorities before scoring.
- **Ignoring Risk**: Option A is cheap, option B is expensive. Choose A. A carries 50% risk of complete failure. **Guard**: Explicitly include risk; risk-adjust scores.
- **Scoring Without Rationale**: "Option A scores 3, option B scores 4." Why? **Guard**: Document scoring rationale; allow stakeholders to challenge.

## Further Reading

- _Decisioning Theory_ — frameworks for structured decision-making
- _Software Architecture Decision Records_ by Michael Nygard — documenting architectural decisions
- _The Phoenix Project_ — understanding system-level trade-offs
