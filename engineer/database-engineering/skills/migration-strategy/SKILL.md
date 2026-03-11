---
name: migration-strategy
description: Safe schema migrations, backward compatibility, zero-downtime deployments, and rollback strategies.
---

# Migration Strategy

Changing schemas safely without breaking applications or downtime.

## Context

You are planning a schema migration. Design for safety; assume rollback is necessary.

## Domain Context

- **Backward Compatible**: Old code still works during migration
- **Forward Compatible**: New code works on old schema during rollout
- **Atomic**: Migration succeeds or fails completely; no partial state
- **Rollback**: Can you undo if something goes wrong?
- **Testing**: Dry run on production-like database

## Instructions

1. **Plan Migration**: What's changing? Is it backward compatible?
2. **Add Column Nullable**: New columns must be nullable initially
3. **Migrate Data**: Fill new column from old if needed
4. **Remove Old Column**: Only after code stops using it
5. **Test Rollback**: Practice rolling back; timing matters
6. **Run on Read Replica**: Test on replica before production
7. **Monitor**: Watch for slow queries from migration locks

## Anti-Patterns

- Blocking migrations during business hours; locks = downtime
- Not testing rollback; assumes everything goes right
- Removing old columns immediately; old code breaks
- No backward compatible transition; lock old code, deploy new together
- Not checking migration speed; ALTER TABLE locks table
- Assuming RENAME COLUMN is free; some databases lock table

## Further Reading

- Django migrations documentation (general principles)
- PostgreSQL ALTER TABLE (what locks tables)
- Facebook's online schema change tool (Onlineschemachange)
