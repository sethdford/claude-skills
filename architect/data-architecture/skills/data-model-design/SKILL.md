---
name: data-model-design
description: Design data models for business domains using entity-relationship or domain-driven design. Use when modeling new domains or refactoring data structures.
---

# Data Model Design

Design data models that correctly represent business domains and support required queries efficiently.

## Context

You are modeling a business domain in a database. The data model must reflect business semantics and perform well.

## Domain Context

Based on relational theory and domain-driven design:

- **Entities**: Things with identity (User, Order)
- **Attributes**: Properties of entities (name, email)
- **Relationships**: How entities connect (User has many Orders)
- **Normalization**: Reduce redundancy; improves write performance
- **Denormalization**: Intentionally duplicate data; improves read performance

## Instructions

1. **Identify Entities**: What are the main concepts? List with primary key.
2. **Identify Attributes**: For each entity, list properties.
3. **Define Relationships**: One-to-one, one-to-many, many-to-many.
4. **Normalize**: Remove update anomalies through normal forms.
5. **Denormalize Strategically**: Add calculated columns or tables for read performance.

## Anti-Patterns

- **Premature Normalization**: Third-normal-form everywhere. Result: slow queries. **Guard**: Design for reads; denormalize if needed.
- **Flat Tables**: No normalization; entity data scattered. Result: update anomalies. **Guard**: At least second-normal-form.

## Further Reading

- _Relational Database Design_ — normalization fundamentals
- _Domain-Driven Design_ — modeling business domains
