---
name: event-sourcing
description: Store state as immutable event log instead of current values. Build auditable, event-driven systems with full history. Use when auditability, temporal queries, or event-driven processing matters.
---

# Event Sourcing

Build auditable systems by storing complete history of state changes as immutable events rather than current values.

## Context

You are designing a system requiring auditability, temporal analysis, or replay capability. Event sourcing provides complete history and enables powerful event-driven architectures. Read domain requirements and existing event-driven patterns.

## Domain Context

Based on Greg Young's event sourcing work and CQRS patterns:

- **Event Store**: Append-only log of domain events; immutable, ordered
- **Aggregate Reconstruction**: Replay events to reconstruct current state on-demand
- **Snapshots**: Optimize replay by storing intermediate state; trade storage for speed
- **Event Versioning**: Events evolve; handle schema changes in replays
- **Projections**: Materialize different views from event stream (CQRS read models)

## Instructions

1. **Identify Core Events**: What state changes matter? Order placed, payment received, shipment dispatched. Each event is fact about domain; captured in past tense.

2. **Design Event Schema**: Each event contains timestamp, aggregate ID, type, data. Include enough context to understand intent (who, when, why).

3. **Plan Aggregate Boundaries**: Group related events into aggregates. Order aggregate: contains all events for single order. Enables consistent snapshots and replay.

4. **Implement Snapshot Strategy**: Full replay from beginning gets slow. Snapshot order state every 100 events; replay only from last snapshot. Balance storage and speed.

5. **Create Read Projections**: Maintain materialized views (current-state, analytics) from event stream. These are caches; can be rebuilt from events anytime.

## Anti-Patterns

- **Event Sourcing Everything**: Overkill for simple systems. Event store adds complexity. **Guard**: Use only when auditability or temporal queries justify cost.
- **Storing Mutable Events**: Treat events as modifiable records. Result: history changes, audit trail meaningless. **Guard**: Events are immutable facts; never modify.
- **No Event Versioning Strategy**: Events change, old replays break. Result: can't handle evolution. **Guard**: Version events; handle multiple versions in replay logic.
- **Ignoring Snapshot Consistency**: Snapshots diverge from event stream. Result: data inconsistency. **Guard**: Snapshots are optimization; rebuild from events periodically to verify.

## Further Reading

- _Event Sourcing_ by Greg Young — foundational patterns and principles
- _Implementing Event Sourcing_ by Vaughn Vernon — practical patterns for building ES systems
- _Event Driven Architecture in Golang_ by Michael Plöd — implementation patterns
