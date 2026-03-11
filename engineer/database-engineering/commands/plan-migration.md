---
description: Plan safe schema migration with backward compatibility and rollback strategy.
argument-hint: [migration-requirement or schema-change]
---

Chain these steps:

1. Use the `migration-strategy` skill to design backward-compatible steps
2. Use the `transaction-management` skill to ensure safety
3. Use the `query-optimization` skill to check for performance impact
4. Generate migration plan with testing and rollback procedures

After completion, ask: "Should we dry-run this migration on a test database first?"
