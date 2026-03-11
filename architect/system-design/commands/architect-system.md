---
description: Design complete system architecture from requirements. Produces C4 diagrams, bounded contexts, and integration specifications.
argument-hint: [problem statement or requirements document]
---

# Architect System

Chain these steps:

1. Use the `system-decomposition` skill to identify business capabilities and define bounded contexts. Ask domain experts about pain points, growth expectations, and team structure.

2. Use the `domain-driven-design` skill to model each context explicitly. Extract ubiquitous language, design aggregates, identify value objects.

3. Use the `microservices-patterns` skill to specify service-to-service communication. For each integration, decide: synchronous (API) or asynchronous (events)? What patterns (saga, circuit breaker, idempotency)?

4. Use the `api-gateway-design` skill to design the client-facing API layer. Specify routing rules, authentication strategy, rate limiting, and response aggregation.

5. Use the `caching-strategy` skill to identify hot data and design caching layers. Specify TTL, invalidation strategy, and acceptable staleness.

## Deliverables

Produce:

- **C4 Context Diagram**: System boundary, external systems, high-level actors
- **C4 Container Diagram**: Service containers, databases, message brokers, external systems
- **Bounded Context Map**: Show each context, upstream/downstream relationships, anti-corruption layers
- **Service Integration Matrix**: For each service pair, specify communication type (sync/async), pattern (RPC, event, saga), and SLA
- **API Specification**: Endpoint paths, request/response schemas, auth requirements, rate limits
- **Data Model Sketch**: Key entities per context, aggregate boundaries, cross-context references

## Critical Thinking Prompts

Before finalizing:

- Are there >3 synchronous hops in any user-facing workflow? (Indicates coupling)
- Which services are "core" (competitive advantage)? Which are "generic" (replaceable)?
- If one service fails, how many user workflows break?
- How many teams will own this? Can each team own 1-2 services without constant coordination?
- What data must be strongly consistent? What can be eventually consistent?

## Follow-Up Commands

- `decompose-monolith` — If migrating from existing system
- `design-api` — To refine API gateway further
- `design-infrastructure` — To plan deployment topology
