---
name: graphql-schema-design
description: GraphQL type systems, queries, mutations, subscriptions, and schema design patterns.
---

# GraphQL Schema Design

Designing GraphQL schemas for flexible, efficient APIs.

## Context

You are designing a GraphQL schema. Think about types, fields, queries, mutations.

## Domain Context

- **Types**: Nouns (User, Order, Product); fields are attributes
- **Queries**: Read operations; no side effects
- **Mutations**: Write operations; return results
- **Subscriptions**: Real-time updates via WebSocket
- **Fragments**: Reusable selections; avoid duplication

## Instructions

1. **Define Types**: User, Order, Product; what fields do they have?
2. **Design Queries**: Root query type; what can clients read?
3. **Design Mutations**: Root mutation type; what can clients change?
4. **Use Enums**: For fixed sets of values (OrderStatus, Role)
5. **Use Interfaces**: For shared fields across types (Node interface)
6. **Plan Subscriptions**: Real-time updates? What events?
7. **Document Null**: Mark required fields with !

## Anti-Patterns

- Over-nesting types; leads to N+1 query problems
- Allowing mutations without auth checks; easy backdoors
- No rate limiting on mutations; clients can spam writes
- Exposing internal IDs directly; abstract away
- Not planning pagination; large result sets kill performance

## Further Reading

- GraphQL spec and best practices
- Apollo GraphQL docs
- Hasura GraphQL patterns
