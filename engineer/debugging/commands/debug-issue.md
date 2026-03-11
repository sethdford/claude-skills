---
description: Systematic debugging combining log analysis and performance profiling.
argument-hint: [error-message or symptom-description]
---

Chain these steps:

1. Use the `systematic-debugging` skill to establish hypothesis
2. Use the `log-analysis` skill to extract timeline and context
3. Use the `performance-profiling` skill to identify bottlenecks if relevant
4. Generate debugging checklist and next steps

After completion, suggest: "Try this hypothesis next, or shall we use binary-search-debugging to isolate the commit?"
