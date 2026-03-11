# assess-coverage

Analyze test coverage and identify gaps.

## Chains

1. **test-coverage-analysis** — Measure coverage and identify gaps
2. **risk-based-test-plan** — Prioritize coverage gaps by risk
3. **test-strategy-design** — Propose targeted tests to fill gaps

## Usage

```
/assess-coverage "Provide coverage report details or code repository"
```

## Expected Output

- Coverage metrics by module/component
- Coverage gap analysis
- Risk assessment of uncovered areas
- Prioritized gap-filling test plan
- Recommendations for reaching coverage targets

## Example

```
/assess-coverage "Backend coverage is 78% overall, but auth module is only 45%.
Error paths and edge cases are largely uncovered. Front-end coverage is 82%."
```

---
