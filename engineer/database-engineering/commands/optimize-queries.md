---
description: Analyze slow queries, identify missing indexes, and rewrite queries for performance.
argument-hint: [slow-query or query-list]
---

Chain these steps:

1. Use the `query-optimization` skill to analyze EXPLAIN PLAN
2. Use the `index-design` skill to suggest missing indexes
3. Use the `schema-design` skill to check for schema issues
4. Generate optimization recommendations with before/after analysis

After completion, ask: "Should we monitor these queries after optimization to verify improvement?"
