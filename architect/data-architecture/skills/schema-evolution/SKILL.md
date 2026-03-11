---
name: schema-evolution
description: Manage database schema changes while maintaining backwards compatibility. Handle migrations, versioning, and zero-downtime deployments. Use when evolving data models in production systems.
---

# Schema Evolution

Evolve database schemas safely while maintaining backwards compatibility and minimizing downtime.

## Context

You are planning schema changes in production systems. Design migrations that don't break deployed clients or services. Read current schemas, deployment frequency, and rollback requirements.

## Domain Context

Based on production database migration best practices:

- **Backwards Compatibility**: Old code continues working with new schema; new code works with both
- **Forwards Compatibility**: New code can read old data; gracefully handles missing fields
- **Zero-Downtime Deployment**: Database changes don't require application downtime
- **Additive Changes**: Adding columns/tables is safe; dropping/renaming requires care
- **Dual-Write Pattern**: Write to both old and new schema during migration; switch reads

## Instructions

1. **Plan Phase 1 (Additive)**: Add new columns/tables. Code ignores new columns for now. Deploy database changes. All existing code still works.

2. **Plan Phase 2 (Dual Write)**: Update application code to write to both old and new schema. Reads can use either. Let data double-write for period (hours to days).

3. **Plan Phase 3 (Migrate Data)**: Background job migrates existing data to new schema. Backfill new fields from old data via transformation.

4. **Plan Phase 4 (Code Switch)**: Update code to read from new schema, write to both. Gradually shift reads: 10% new, 90% old → 50/50 → 100% new.

5. **Plan Phase 5 (Cleanup)**: Once all code reads new schema, remove old schema if safe. Keep removal as separate deployment after week of monitoring.

## Anti-Patterns

- **Big-Bang Migration**: Deploy schema and code changes simultaneously. Result: downtime, hard rollback. **Guard**: Separate database and application deployments; deploy database first.
- **Dropping Columns Without Wrapping Code**: Assume all code updated. Result: errors in production. **Guard**: Wait 1+ releases before drop; deploy code removal first, schema cleanup second.
- **No Rollback Plan**: Assume migrations succeed. Result: stuck in bad state. **Guard**: Practice rollbacks; keep old schema for period; verify data integrity.
- **Ignoring Hot Data**: Migrate huge table in single pass. Result: locks, downtime. **Guard**: Use online migration tools (pt-online-schema-change, pg-repack); batch smaller tables.

## Further Reading

- _Database Reliability Engineering_ by Laine Campbell and Charity Majors — schema migration strategies
- _PostgreSQL Documentation on ALTER TABLE_ — database-specific migration patterns
- _Zero Downtime Deployments_ — architectural patterns for safe releases
