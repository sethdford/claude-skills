---
name: architecture-anti-patterns
description: Identify and avoid common architectural mistakes. Recognize patterns of failure. Use when reviewing designs or learning from mistakes.
---

# Architecture Anti-Patterns

Recognize and avoid common architectural mistakes that lead to fragility, complexity, or failure.

## Context

You are reviewing an architecture and want to spot common anti-patterns. Patterns of failure repeat across organizations. Learn them, recognize them, guide teams away from them.

## Domain Context

Based on architecture and design anti-patterns research:

- **God Object**: One class/service responsible for too much. Hard to change, test, understand.
- **Big Ball of Mud**: No clear architecture. Code accretion with no structure. Hard to modify without breaking things.
- **Circular Dependency**: A depends on B, B depends on A. Can't use A without B, vice versa. Breaks modularity.
- **Database as Integration Point**: Services share database schema. Schema changes break all services. No independence.
- **Premature Optimization**: Design for 10x scale when you have 1x. Overcomplex, unmaintainable.

## Instructions

1. **Common Anti-Patterns and Recognition**:
   - **Monolith Bloat**: Hundreds of thousands of lines in one service. Deploys take 30 min. Hard to test. Fix: decompose into services by business domain.
   - **Tight Coupling**: Service A calls Service B calls Service C synchronously. Cascade failure: A down → B unavailable → C affected. Fix: async, timeouts, circuit breakers, fallbacks.
   - **No Logging/Monitoring**: Don't know what's happening in production. Outage takes hours to debug. Fix: structured logging, metrics, distributed tracing, alerts.
   - **Cache Invalidation Chaos**: Cache stale data, inconsistency everywhere. Fix: cache strategy with TTL, event-driven invalidation, don't cache mutable shared state.
   - **N+1 Query Problem**: Loop calls database for each item. 1000 items = 1000 queries. Fix: batch queries, join tables, fetch aggregates.

2. **Diagnose When Present**:
   - Performance issues in service you don't touch? Likely tight coupling or cascade failure.
   - Hard to understand request path? Likely circular dependencies or god objects.
   - Frequent outages from unrelated changes? Likely shared database or tight coupling.

3. **Guide Teams Away**:
   - "I'm seeing patterns here that might make this hard to evolve. Let's consider [alternative]."
   - Show concrete consequences: "Shared database means we can't deploy Customer service without coordinating with Order service."

## Anti-Patterns of Anti-Pattern Avoidance

- **Over-Applying Patterns**: Every design must be microservices, event-driven, etc. Result: overengineering. **Guard**: Patterns are tools; choose based on problem, not pattern preference.
- **Learning Too Late**: Hit anti-pattern, then refactor. Result: wasted effort, technical debt. **Guard**: Recognize early; course-correct before pattern takes root.
- **Ignoring Team Capabilities**: Apply advanced pattern (CQRS, event sourcing) without team expertise. Result: bugs, performance issues. **Guard**: Match pattern to team skill; invest in learning.

## Further Reading

- _AntiPatterns: Refactoring Software, Architectures, and Projects in Crisis_ by William H. Brown et al. — comprehensive anti-patterns
- _Building Microservices_ by Sam Newman — anti-patterns in microservice design
- _Release It!_ by Michael Nygard — production anti-patterns
