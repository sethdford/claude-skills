---
description: Safe refactoring combining refactoring-catalog and dependency-injection patterns.
argument-hint: [code-block or file-path]
---

Chain these steps:

1. Use the `refactoring-catalog` skill to identify low-risk refactorings (Extract Method, Replace Temp with Query)
2. Use the `dependency-injection` skill to evaluate coupling and suggest DI opportunities
3. Propose refactorings in order of impact; start with Extract Method to reduce complexity
4. Generate refactored code with clear before/after comparison

After completion, suggest: "Next, use the `review-code` command to verify the refactoring improves overall quality."
