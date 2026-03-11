---
description: Comprehensive code review combining clean-code-review and code-smell-detector.
argument-hint: [code-block or file-path]
---

Chain these steps:

1. Use the `clean-code-review` skill to assess naming, function design, comments, and formatting
2. Use the `code-smell-detector` skill to identify long methods, duplication, and low cohesion
3. Synthesize findings into a prioritized list: critical issues first (duplication, error handling), then improvements (naming, complexity)
4. Suggest specific refactorings with before/after examples

After completion, ask: "Would you like me to help refactor any of these issues?" and suggest the `refactor` command.
