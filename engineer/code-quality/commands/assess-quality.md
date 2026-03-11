---
description: Full quality assessment combining code-complexity-analysis, naming-conventions, and error-handling-patterns.
argument-hint: [code-block or file-path]
---

Chain these steps:

1. Use the `code-complexity-analysis` skill to measure cyclomatic and cognitive complexity
2. Use the `naming-conventions` skill to evaluate variable, function, and class names
3. Use the `error-handling-patterns` skill to assess error handling strategy
4. Synthesize into a quality score (1-10) with specific, actionable recommendations

After completion, ask: "Which area would you like to improve first?" and suggest the `refactor` command for the highest-impact issues.
