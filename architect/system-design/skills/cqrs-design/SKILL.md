---
name: cqrs-design
description: Separate command (write) and query (read) models for complex domains. Use when read/write patterns diverge significantly or when audit/consistency requirements demand immutability.
---

# CQRS Design

Implement Command Query Responsibility Segregation (CQRS) to align data models with actual usage patterns and enable independent scaling of reads and writes.

## Context

You are designing or refactoring a system with complex read and write patterns. The user faces performance issues, audit requirements, or divergent read/write needs. Read their current data access patterns.

## Domain Context

Based on Greg Young's CQRS work and Fowler's research:

- **Command Side**: Optimized for writes; enforces business rules; maintains single source of truth
- **Query Side**: Optimized for reads; denormalized for performance; eventual consistency acceptable
- **Event Sourcing**: Often paired with CQRS; commands generate events, events drive queries
- **Read Models**: Projections built from events; can be recreated from command side state
- **Consistency Boundary**: Commands are strongly consistent within aggregate; queries lag slightly

## Instructions

1. **Analyze Read vs Write**: List all queries used; identify divergences from write model. Example: commands work with Orders (with line items), but queries need denormalized OrderSummary (customer name, total, status).

2. **Design Command Model**: Optimize for consistency and rule enforcement. Aggregate should protect invariants. Example: Order aggregate ensures total ≥ sum of items.

3. **Design Read Models**: For each query pattern, denormalize to minimize joins. Example: OrderSummary includes customer name (copied from command), total (calculated), status (current).

4. **Define Synchronization**: How does read model stay updated? Options:
   - **Event-Driven**: Commands emit events; readers consume and project
   - **Change Data Capture**: Trigger-based updates from command database
   - **Polling**: Periodically sync from command to read schema

5. **Handle Eventual Consistency**: Users must accept slight staleness. Define lag threshold (e.g., reads lag writes by max 2 seconds). Show stale data indicator if lag exceeds threshold.

## Anti-Patterns

- **CQRS Without Event Sourcing**: Creates two databases that drift out of sync. Result: questions about truth. **Guard**: Pair CQRS with event sourcing or CDC to keep models synchronized.
- **Premature CQRS**: Added complexity without read/write divergence. Result: boilerplate with no benefit. **Guard**: Only apply CQRS when read and write models naturally differ.
- **Ignoring Consistency Window**: Treats read model as synchronous. Result: users see stale data and complain. **Guard**: Define maximum staleness; make it visible in UI (e.g., "Last updated 2 seconds ago").
- **Over-Denormalization**: Read model includes every possible field. Result: maintenance nightmare and slow projections. **Guard**: Design read models per query; allow multiple read models.

## Further Reading

- _Exploring CQRS and Event Sourcing_ by Greg Young — foundational concepts
- _Microservices Patterns_ by Chris Richardson — CQRS in microservices context
- _Enterprise Integration Patterns_ — event-driven projections and synchronization
