---
description: Design comprehensive API testing strategy including contracts and integration tests.
argument-hint: [api-schema or existing-api]
---

Chain these steps:

1. Use the `api-testing-strategy` skill to plan test layers
2. Use the `api-error-handling` skill to ensure error cases are tested
3. Use the `rest-api-design` skill (or graphql) to verify semantic correctness
4. Generate test plan with contract tests, integration tests, and chaos scenarios

After completion, ask: "Should we implement these tests now, or start with contract tests?"
