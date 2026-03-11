---
name: event-driven-architecture
description: Design systems that communicate through events instead of direct service calls. Use when building loosely-coupled, scalable, and resilient architectures.
---

# Event-Driven Architecture

Build systems where services communicate through immutable events, enabling loose coupling and independent scaling.

## Context

You are designing an event-driven system. The user is building integrations across services or needs to decouple components. Read their current architecture and integration patterns.

## Domain Context

Based on Gregor Hohpe's Enterprise Integration Patterns and modern event-driven research:

- **Event Sourcing**: Store state as append-only event log; reconstruct state by replaying events
- **Event Bus**: Central publish-subscribe; services emit domain events, others react independently
- **Choreography vs Orchestration**: Choreography = services react to events independently; orchestration = central coordinator directs flow
- **Exactly-Once Semantics**: Guarantee each event is processed once; requires deduplication at consumer
- **Event Versioning**: Events evolve over time; old and new consumers must coexist

## Instructions

1. **Define Events**: For each business process, identify events (UserCreated, OrderPlaced, PaymentProcessed). Include: timestamp, aggregate ID, payload, version.

2. **Design Producer & Consumer**: For each service that publishes events, specify topic/channel. For consumers, specify subscription and reaction. Include idempotency key for deduplication.

3. **Choose Messaging Infrastructure**: Event bus (RabbitMQ, Kafka, SNS) vs database change data capture (CDC). Bus is simpler, CDC couples to database.

4. **Handle Event Versioning**: Publish event version. Consumers validate schema; ignore unknown fields. Plan rollout: old consumers coexist with new producers for transition period.

5. **Establish Observability**: Track event publication latency, consumer lag, dead letter queues (failed events). Alert on lag > threshold.

## Anti-Patterns

- **Synchronous RPC Over Event Bus**: Treats event bus like RPC (request-reply). Result: waiting for responses, tight coupling. **Guard**: Events are fire-and-forget; never wait for a response.
- **Event As Database Query**: Sends events like "GetUser" and waits. **Guard**: Events record facts ("UserCreated"), never request actions ("FetchUser").
- **No Event Schema**: Events evolve chaotically without versioning. Result: incompatible producers and consumers. **Guard**: Require schema registry; validate all events.
- **Lost Events on Consumer Failure**: Consumer crashes, event is lost. **Guard**: Require acknowledgment-based delivery (Kafka); never auto-ack.

## Further Reading

- _Enterprise Integration Patterns_ by Gregor Hohpe and Bobby Woolf — comprehensive pattern catalog
- _Building Event-Driven Microservices_ by Adam Bellemare — practical event design and architecture
- _Designing Data-Intensive Applications_ by Martin Kleppmann — event sourcing and streaming foundations
