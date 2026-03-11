---
name: schema-design
description: Database schema design with normalization, relationships, constraints, and data integrity.
---

# Schema Design

Designing schemas that are correct, performant, and maintainable.

## Context

You are designing a database schema. Plan for data integrity and query patterns.

## Domain Context

- **Normalization**: 1NF, 2NF, 3NF; eliminate anomalies
- **Keys**: Primary keys, foreign keys, unique constraints
- **Types**: Choose appropriate column types; int vs bigint matters
- **Constraints**: NOT NULL, UNIQUE, CHECK enforce data integrity
- **Indexes**: Think about query patterns upfront

## Instructions

1. **Identify Entities**: What nouns? User, Order, Product?
2. **Identify Relationships**: One-to-many, many-to-many?
3. **Normalize**: 3NF typical; reduce duplication
4. **Keys**: Primary key on each table; foreign keys for relationships
5. **Types**: int for IDs, text for strings, jsonb for semi-structured
6. **Constraints**: Enforce data integrity at database level
7. **Indexes**: Plan indexes for common queries

## Anti-Patterns

- No primary keys; can't uniquely identify rows
- Storing arrays/lists in columns; use junction tables
- Text columns for numbers; use appropriate types
- No foreign keys; data integrity is application's problem
- Too much normalization; separate tables hurt performance
- No constraints; garbage data gets inserted

## Further Reading

- C.J. Date, _An Introduction to Database Systems_
- PostgreSQL schema design documentation
- Star schema (data warehouse design)
