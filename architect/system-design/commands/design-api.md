---
description: Create API gateway and service contract specifications. Design scalable APIs.
argument-hint: [backend services or existing API]
---

# Design API

Chain these steps:

1. Use the `api-gateway-design` skill to define gateway responsibilities: routing, auth, rate limiting, aggregation. Map API paths to backend services.

2. Use the `cqrs-design` skill to design read vs write models. Identify queries that need denormalization. Specify read model update strategy (event-driven or CDC).

3. Use the `microservices-patterns` skill to specify resilience for each backend call. Include circuit breaker, retry, timeout, bulkhead for every downstream service.

4. Use the `caching-strategy` skill to identify cacheable responses. Specify cache layers (client, edge, service) and invalidation strategy.

5. Use the `domain-driven-design` skill to ensure API vocabulary matches ubiquitous language. Avoid implementation-specific terms (UserService, OrderService); use domain terms.

## Deliverables

Produce:

- **API Specification**: OpenAPI 3.0 with endpoint paths, HTTP methods, request/response schemas, error codes
- **Gateway Configuration**: Routing rules (path → service), auth strategy, rate limits (per-user, per-API, per-endpoint)
- **Response Aggregation Matrix**: For each endpoint, identify services to call. Specify parallelization (fan-out), ordering, error handling.
- **Cache Policy Matrix**: For each endpoint, specify cache layer (client/edge/service), TTL, invalidation trigger
- **Resilience Configuration**: For each downstream service call, specify timeout, circuit breaker threshold (error rate, response time), retry policy (max attempts, backoff)

## Critical Thinking Prompts

Before finalizing:

- Can a client make the request in <500ms? If not, which services are slow? Aggregate at gateway instead?
- What happens if a downstream service is unavailable? Does the entire endpoint fail or degrade?
- Are you caching User data for 5 minutes while user might change it? Is stale acceptable?
- Do you validate JWT on every request (auth bottleneck) or cache validation?
- What's the gateway's SLA? If it goes down, how many clients fail?

## Follow-Up Commands

- `architect-system` — Design remaining services
- `design-infrastructure` — Plan API gateway deployment
- `evaluate-architecture` — Audit API performance after deployment
