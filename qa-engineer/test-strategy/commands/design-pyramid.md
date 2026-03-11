# design-pyramid

Design a test pyramid architecture for a project.

## Chains

1. **test-pyramid-design** — Design pyramid structure and distribution
2. **automation-architecture** — Plan automation framework strategy
3. **test-strategy-design** — Align pyramid with overall test strategy

## Usage

```
/design-pyramid "Describe your architecture (monolith, microservices, etc.) and current testing"
```

## Expected Output

- Test pyramid diagram with recommended distribution
- Rationale for distribution percentages
- Test strategy for each level (unit, integration, E2E)
- Tool and framework recommendations
- Implementation roadmap

## Example

```
/design-pyramid "Microservices architecture with 15 services, React frontend.
Currently: many E2E tests, few unit tests. Manual integration testing.
Want: faster feedback, more stable suites."
```

---
