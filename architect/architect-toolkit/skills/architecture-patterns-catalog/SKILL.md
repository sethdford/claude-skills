---
name: architecture-patterns-catalog
description: Reference catalog of proven architecture patterns. Know when to apply each pattern, tradeoffs, and examples. Use as reference when designing systems.
---

# Architecture Patterns Catalog

Curated reference of proven patterns with guidance on when and how to apply them.

## Context

You are designing a system and want to know proven patterns that solve your problem. Reference catalog of patterns: when to use, tradeoffs, real-world examples.

## Domain Context

Based on pattern catalogs (Gang of Four, Enterprise Patterns, Domain-Driven Design):

- **Structural Patterns**: How components fit together (Adapter, Facade, Bridge)
- **Behavioral Patterns**: How components interact (Observer, Strategy, State)
- **Architectural Patterns**: System-level patterns (Microservices, Event-Driven, CQRS)
- **Data Patterns**: How data flows (ETL, CDC, Event Sourcing)
- **Messaging Patterns**: How services communicate (Request-Reply, Pub-Sub, Saga)

## Pattern Categories with Examples

1. **Communication Patterns**:
   - **Synchronous (Request-Reply)**: REST, gRPC. Blocking, tight coupling, simple.
   - **Asynchronous (Pub-Sub)**: Message broker, events. Loose coupling, eventual consistency.
   - **Saga Pattern**: Distributed transaction across services. Orchestrator vs choreographer.

2. **Data Patterns**:
   - **Event Sourcing**: Store events as source of truth. Auditability, temporal queries, replay.
   - **CQRS**: Separate read and write models. Scalability, complexity.
   - **Polyglot Persistence**: Different databases for different workloads. Flexibility, operational complexity.

3. **Resilience Patterns**:
   - **Circuit Breaker**: Stop calling failing service, fast-fail. Prevent cascade failure.
   - **Bulkhead**: Isolate resources (threads, connections). One service failure doesn't starve others.
   - **Retry with Backoff**: Retry with exponential backoff. Transient failures recover.

4. **Scalability Patterns**:
   - **Sharding**: Partition data across databases. Horizontal scaling, complexity.
   - **Caching**: Cache hot data. Latency, consistency trade-off.
   - **Load Balancing**: Distribute across instances. Horizontal scaling.

## Instructions

1. **Identify Problem**: What are you trying to solve? Scaling? Reliability? Loose coupling?

2. **Search Catalog**: What patterns address this problem?

3. **Evaluate Trade-offs**: Benefits vs complexity? Team capability? Do we have the infrastructure?

4. **Choose Pattern(s)**: Often combine patterns. Saga + Circuit Breaker. Sharding + Replication.

5. **Implement Carefully**: Patterns solve some problems, create others. Monitor carefully.

6. **Document**: Why you chose this pattern. What trade-offs accepted. What could go wrong.

## Anti-Patterns in Pattern Use

- **Pattern Memorization Without Understanding**: Apply pattern because it's trendy. Result: wrong for problem. **Guard**: Understand pattern's purpose; ensure problem matches.
- **Overusing One Pattern**: Everything is microservices or event-driven. Result: wrong tool for job. **Guard**: Different problems, different patterns.
- **Incomplete Implementation**: Use circuit breaker but not monitoring. Result: fails silently. **Guard**: Implement full pattern; test failure scenarios.
- **No Evolution Path**: Choose pattern, stuck with it forever. Result: outdated, painful. **Guard**: Design to evolve; refactor when costs exceed benefits.

## Further Reading

- _Design Patterns: Elements of Reusable Object-Oriented Software_ by Gang of Four — foundational patterns
- _Enterprise Integration Patterns_ by Gregor Hohpe — messaging and integration patterns
- _Building Microservices_ by Sam Newman — microservice patterns
- _Patterns of Enterprise Application Architecture_ by Martin Fowler — application architecture patterns
