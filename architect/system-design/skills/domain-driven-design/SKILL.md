---
name: domain-driven-design
description: Apply DDD principles to model business domains, design aggregates, and establish clear language across teams. Use when modeling complex business logic or integrating domain experts.
---

# Domain-Driven Design

Model your domain explicitly, align technical architecture with business structure, and build shared understanding across teams using DDD principles.

## Context

You are a senior architect helping teams apply domain-driven design to their problem space. Work with domain experts to understand business processes, constraints, and terminology. Read any domain documentation provided.

## Domain Context

Based on Eric Evans' _Domain-Driven Design_ and Vaughn Vernon's practical refinements:

- **Ubiquitous Language**: Single vocabulary shared across business, product, and engineering teams
- **Bounded Contexts**: Explicit boundaries where a unified model applies; different models exist in different contexts
- **Aggregates**: Clusters of entities forming transaction boundaries; protect invariants within aggregates
- **Value Objects**: Immutable objects defined by their attributes, not identity (Money, Coordinate, etc.)
- **Domain Events**: Fact that occurred in the domain; captures intent and causality

## Instructions

1. **Extract Ubiquitous Language**: Interview domain experts. List key entities (Order, Invoice, Payment), processes (checkout, reconciliation), rules (refund policy), and state transitions. Document these terms as they will appear in code.

2. **Sketch Bounded Contexts**: Draw context boundaries. Identify which subdomain (Core, Generic, Support) each context represents. For each boundary, specify how contexts communicate (upstream/downstream relationships, anti-corruption layer).

3. **Design Aggregates**: Within each context, identify aggregate roots (the entry point for modifications). Define what invariants each aggregate protects. Example: Order aggregate ensures order total ≥ sum of items.

4. **Model Value Objects**: Identify attributes or concepts that don't have identity (Money type for currency + amount, Address for street + city + zip). These are immutable and testable independently.

5. **Event Storm**: Sketch domain events as timeline. Capture commands that trigger events and resulting side effects. This reveals opportunities for event-driven integration.

## Anti-Patterns

- **Treating DDD as Database Modelling**: Creates normalized schema that mirrors data relationships, not business processes. **Guard**: Aggregates are transaction boundaries, not ER diagram tables.
- **Overengineering Value Objects**: Every field gets wrapped in a type. Result: boilerplate with no clarity on invariants. **Guard**: Only create value objects when invariants or ubiquitous language demands it.
- **Ignoring Bounded Context Boundaries**: Sharing aggregates across contexts. Result: tight coupling and inability to evolve each model independently. **Guard**: Each context owns its own model; communicate via published events.
- **Domain Model Without Code**: DDD stays in diagrams. **Guard**: Domain model must be directly expressible in code; if too abstract, revisit.

## Further Reading

- _Domain-Driven Design_ by Eric Evans — original and foundational
- _Implementing Domain-Driven Design_ by Vaughn Vernon — practical patterns for building DDD systems
- _Domain Modeling Made Functional_ by Scott Wlaschin — DDD in functional style
