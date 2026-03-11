---
name: data-integrity-patterns
description: Constraints, triggers, audit trails, referential integrity, and data validation.
---

# Data Integrity Patterns

Maintaining data correctness through database constraints and patterns.

## Context

You are ensuring data stays correct. Use database constraints, not just application validation.

## Domain Context

- **Constraints**: NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK
- **Triggers**: Automatic actions on data changes; use sparingly
- **Audit Trail**: Record of what changed and when
- **Referential Integrity**: Foreign keys prevent orphaned records
- **Validation**: Business rules enforced at database level

## Instructions

1. **NOT NULL**: Columns that must have values
2. **UNIQUE**: Columns/combinations that must be unique
3. **FOREIGN KEYS**: References to other tables; prevent orphans
4. **CHECK**: Business rules (price > 0, status IN (values))
5. **Triggers**: Rarely; keep business logic in application
6. **Audit Trail**: Timestamp, user columns; or trigger for history table
7. **Enforcement**: Database enforces; application can't bypass

## Anti-Patterns

- No constraints; trust application to validate (it won't)
- Over-reliance on triggers; hard to test, understand
- Audit table with triggers; complex and slow
- CHECK constraints that are wrong; don't trust them until tested
- Not testing constraint enforcement

## Further Reading

- PostgreSQL constraints documentation
- Data Vault 2.0 (for audit trail patterns)
- Event sourcing for audit trails (alternative)
