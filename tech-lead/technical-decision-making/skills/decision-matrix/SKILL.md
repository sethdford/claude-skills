---
name: decision-matrix
description: Use weighted criteria matrices to systematically compare options and make defensible technical decisions. Use when evaluating competing approaches or vendors.
---

# Decision Matrix

Build scoring matrices that make tradeoffs visible and defensible, replacing gut-feel decisions with systematic analysis.

## Context

You are a senior tech lead making a decision for $ARGUMENTS using multiple competing options. Decision matrices force clarity on criteria, prevent bike-shedding, and create accountability.

## Domain Context

- **Explicit criteria beats implicit** — unstated preferences lead to endless debate. Written criteria end it. "We value performance over cost" is debatable; "performance weights 40%, cost 25%" is objective.
- **Weighting reveals values** — how you weight criteria shows what your organization truly prioritizes. Make it explicit so everyone can question it.
- **Numerical scoring prevents ties** — when everything scores 7/10, you need tiebreaker logic. Build it into the matrix (e.g., "if tied, prefer lower cost").
- **Options should be mutually exclusive** — if not, combine them. If considering options A, B, and A+B, you're confused about boundaries.

## Instructions

1. **List options**: Clearly name each option competing. Example: "Use Postgres" vs "Use DynamoDB" vs "Use MongoDB". Make sure these are truly alternative choices, not variations of same choice.

2. **Define criteria**: List 6-10 weighted factors. Example: performance (40%), cost (25%), team capability (20%), vendor lock-in risk (10%), time-to-delivery (5%). Weights should sum to 100. Make criteria mutually exclusive (not "performance and speed" which overlap).

3. **Score each option**: On each criterion, score option A, B, C on 0-10 scale. Document your reasoning. "Performance (Postgres 8/10 due to proven scalability for our scale, DynamoDB 7/10 due to operational unknowns, MongoDB 6/10 due to memory overhead)."

4. **Calculate weighted score**: Score × weight for each criterion, sum across all criteria per option. Option with highest score wins. Example: Postgres 8.2/10 weighted score, DynamoDB 7.1, MongoDB 6.5.

5. **Document tradeoffs**: "Postgres wins decisively. Closest alternative is DynamoDB with 1.1-point gap. Gap is meaningful; DynamoDB doesn't lose on any major criterion, just accumulates small losses. If vendor lock-in risk becomes critical, revisit."

## Anti-Patterns

- **Gaming the matrix**: Designing weights so predetermined choice wins. If you already know the answer, why matrix? Use transparent criteria or admit the decision was made politically.
- **Too many criteria**: 15+ factors become meaningless. Combine overlapping criteria. Stick to 6-10 that truly differentiate options.
- **Scores without reasoning**: "Postgres 8/10" without explanation. Why not 7? Why not 9? Document reasoning. It justifies the score and educates observers.
- **Ignoring outliers**: One option scores best overall but terrible on one criterion ("Cost is 100x more expensive but performance is excellent"). Callout outliers explicitly. Decision should reflect whether you'll accept that tradeoff.
- **Matrix as final arbiter**: Treating matrix score as absolute truth ("Matrix says option A, so that's the decision"). Use matrix to inform, not to replace judgment. If score surprises you, examine the criteria or scores.

## Further Reading

- "Decision Matrices" (GRID International) — build and use matrices effectively
- _Thinking, Fast and Slow_ (Kahneman) — how structured decisions beat gut feel
- _Decisive_ (Heath brothers) — multiple options improve decision quality
- "Multi-Criteria Decision Analysis" (Wikipedia/academic) — formal matrix theory
