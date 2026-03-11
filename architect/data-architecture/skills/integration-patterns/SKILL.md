---
name: integration-patterns
description: Integrate data across systems using ETL, CDC, event streaming, and API patterns. Design robust, maintainable data integrations. Use when connecting disparate data sources or microservices.
---

# Integration Patterns

Design robust data integrations between systems using time-tested patterns and technologies.

## Context

You are integrating data from multiple systems. Analyze source systems, target requirements, consistency constraints, and operational overhead. Read existing integration code or architecture documents.

## Domain Context

Based on Gregor Hohpe's _Enterprise Integration Patterns_ and modern streaming:

- **ETL (Extract-Transform-Load)**: Scheduled batch jobs; simple but high latency
- **ELT (Extract-Load-Transform)**: Load raw data first, transform in warehouse; flexible but storage intensive
- **CDC (Change Data Capture)**: Capture database changes in realtime; high fidelity but complex
- **Event Streaming**: Publish domain events to message brokers; loosely coupled but at-least-once semantics
- **API-Based Integration**: Synchronous queries; simple but tightly coupled and slower

## Instructions

1. **Choose Primary Pattern**: Batch ETL (cost-effective, simple)? CDC (realtime, high fidelity)? Event streams (loosely coupled, asynchronous)? Synchronous APIs (simple, tight coupling)? Often hybrid approach.

2. **Design Idempotency**: Ensure processing same data twice yields same result. Use unique identifiers, deduplication logic, or transactional sinks.

3. **Handle Schema Evolution**: Source schema changes. Build transformation layer that's resilient to new fields, deprecated fields, type changes.

4. **Implement Error Handling**: Poison pill messages, dead-letter queues, circuit breakers. Log failures with context for debugging and replay.

5. **Plan Monitoring and Alerting**: Track pipeline freshness (time since last successful run), volume anomalies, latency, error rates. Alert on SLA violations.

## Anti-Patterns

- **Direct Database-to-Database Integration**: Source DB talks directly to sink. Result: tight coupling, hard to recover from failures, operational complexity. **Guard**: Introduce message queue or ETL layer for decoupling.
- **No Idempotency Guarantees**: Retry logic assumes exactly-once delivery. Result: duplicate data, inconsistency. **Guard**: Always design for at-least-once; implement idempotency at sink.
- **Ignoring Backpressure**: Source pushes data faster than sink can consume. Result: memory buildup, crashes. **Guard**: Implement queueing, rate limiting, or load shedding.
- **Monolithic Transformation Logic**: All business logic in single transformation. Result: hard to test, reuse, evolve. **Guard**: Break into modular stages; test each independently.

## Further Reading

- _Enterprise Integration Patterns_ by Gregor Hohpe and Bobby Woolf — foundational patterns
- _Designing Event-Driven Systems_ by Ben Stopford — event-based integration
- _Kafka: The Definitive Guide_ by Neha Narkhede — modern stream-based integration
