---
name: monolith-assessment
description: Evaluate whether to keep, refactor, or break apart a monolithic system. Use when facing scaling or team velocity challenges with monoliths.
---

# Monolith Assessment

Systematically evaluate a monolithic system to determine the right evolution path: stay monolith, strangler fig, distributed monolith, or true microservices.

## Context

You are analyzing a monolithic system. The user is experiencing pain (scaling, slow deployment, team conflicts) and needs objective guidance on whether to split services or optimize the monolith. Read code samples, deployment info, and team structure.

## Domain Context

Based on Sam Newman, Martin Fowler, and Shopify's monolith journey:

- **Two-Pizza Team Rule**: Effective team size for one codebase is ~8-10 engineers; beyond that, splitting accelerates
- **Deployment Coupling**: Cannot deploy independently → services should separate
- **Data Coupling**: Services share databases → integration tighter than desired
- **Strangler Fig Pattern**: Incrementally replace monolith pieces without full rewrite
- **Inverse Conway's Law**: System architecture mirrors team structure; if teams are independent, system should be

## Instructions

1. **Score Pain Dimensions**: Rate the monolith on (1-5): deployment frequency, team wait times, scaling per component, technology brittleness. High scores indicate split pressure.

2. **Map Team Structure**: How many teams? Do they work independently? Are code conflicts blocking? If >3 teams, monolith is likely bottleneck.

3. **Identify Seams**: Find natural split points (feature flags, database views isolating concerns, API boundaries). Ask: "Could I change this without touching that?"

4. **Cost-Benefit Analysis**: For each proposed split, calculate: split cost (effort + infrastructure), benefit (deployment frequency +X%, scaling independently, team autonomy). Use threshold: benefit > 3x cost.

5. **Choose Evolution Path**:
   - **Stay Monolith**: If pain is low and splits cost high, optimize in-place
   - **Modular Monolith**: Separate deployable modules within single process
   - **Strangler Fig**: Gradually extract services while maintaining monolith
   - **Distributed**: Split if benefits clearly outweigh costs

## Anti-Patterns

- **Splitting Because It's Trendy**: "Microservices are the future" without measuring pain. Result: distributed monolith with no benefit. **Guard**: Only split when pain exceeds cost.
- **Database Per Service Too Early**: Couples services through shared write schema before proving the need. **Guard**: Start with database seams (views, tables); split database only if scaling demands it.
- **Ignoring Team Structure**: Architecture and team don't align. Result: constant cross-team coordination. **Guard**: Design system structure to match desired team structure.
- **Underestimating Infrastructure Cost**: Assumes microservices cost the same to operate. **Guard**: Include containerization, orchestration, observability in cost calculation.

## Further Reading

- _Building Microservices_ by Sam Newman — assessment and strangler fig patterns
- _Monolith to Microservices_ by Sam Newman — migration playbook
- _Shopify's Journey to Microservices_ — case study on monolith optimization and strategic splits
