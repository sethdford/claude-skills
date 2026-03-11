---
name: microservices-patterns
description: Apply proven microservices patterns including saga, circuit breaker, bulkhead, and eventual consistency. Use when designing service-to-service communication and handling distributed failures.
---

# Microservices Patterns

Master distributed system patterns that enable loose coupling, resilience, and independent deployability across service boundaries.

## Context

You are an architect designing microservices interactions. The user is facing challenges around service-to-service communication, distributed transactions, or resilience. Read their current architecture and pain points.

## Domain Context

Based on Chris Richardson's Microservices Patterns and Sam Newman's work:

- **Saga Pattern**: Coordinate distributed transactions without 2PC; break into choreography (event-driven) or orchestration (central coordinator)
- **Circuit Breaker**: Fail fast when downstream service is unavailable; prevent cascading failures
- **Bulkhead Pattern**: Isolate thread pools/resources per service to prevent one slow service from impacting others
- **Eventual Consistency**: Accept stale reads at service boundaries; couple through events, not synchronous calls
- **Idempotency Keys**: Every operation is idempotent; safe to retry without duplicating side effects

## Instructions

1. **Map Distributed Transactions**: Identify workflows crossing service boundaries (e.g., payment → inventory → shipping). For each, decide: synchronous (API call) or asynchronous (events)?

2. **Choose Saga Style**: If async needed, choose choreography (services emit events, others listen) or orchestration (central coordinator). Choreography is loose coupling; orchestration is easier to debug.

3. **Apply Resilience Patterns**: For every sync call, specify circuit breaker thresholds (failure rate, response time). Define bulkheads (thread pool per downstream service). Specify fallback behavior.

4. **Design Idempotency**: For every state-changing operation, define idempotency key (deduplication window). Ensure operations are truly idempotent; don't rely on "at most once" delivery.

5. **Establish Observability**: Define tracing across services (correlation ID at entry point). Log saga execution state. Alert on circuit breaker trips.

## Anti-Patterns

- **Synchronous Everything**: Services call every dependency synchronously. Result: tight coupling, cascading failures, poor resilience. **Guard**: Use events for non-critical updates; sync only for consistency boundaries.
- **Ignoring Idempotency**: Assumes "call it once" safety. Result: duplicate charges, duplicate orders on retries. **Guard**: Every operation must be idempotent; require idempotency key for all mutations.
- **Circuit Breaker Without Fallback**: Opens circuit but doesn't specify what to do. Result: errors propagate, users see failures. **Guard**: Every circuit breaker has a fallback (cached value, degraded mode, user-visible wait).
- **No Correlation IDs**: Cannot trace request across services. **Guard**: Every entry point injects correlation ID; all logs include it.

## Further Reading

- _Microservices Patterns_ by Chris Richardson — comprehensive catalog with patterns and anti-patterns
- _Building Microservices_ by Sam Newman — practical integration and communication strategies
- _Release It!_ by Michael Nygard — resilience patterns and cascading failure prevention
