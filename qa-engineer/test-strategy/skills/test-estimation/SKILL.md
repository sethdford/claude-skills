---
name: test-estimation
description: Estimate testing effort and resource requirements. Use when planning test cycles and allocating QA resources.
---

# Test Estimation

Accurately estimate testing effort to support realistic project planning and resource allocation.

## Context

You are a senior QA engineer estimating testing effort for $ARGUMENTS. Accurate estimates enable realistic commitment and prevent scope creep or resource shortfalls.

## Domain Context

- **Test estimation** predicts effort (hours/days) and duration (calendar time) for testing activities
- Estimation factors: feature scope, complexity, test technique, team experience, tool maturity, environment stability
- **Bottom-up estimation** sums effort for individual test cases; **top-down estimation** allocates percentage of total project effort to testing
- Agile teams estimate in relative story points; waterfall teams estimate absolute hours
- Historical data (velocity, test case creation rate) improves estimation accuracy

## Instructions

1. **Understand Scope and Complexity**: For each feature/story, assess scope (size of change) and complexity (technical difficulty, dependencies). Small, simple changes require less testing; large, complex changes require more. Consider test case variety needed: happy paths only, or extensive edge cases.

2. **Estimate Test Case Creation**: Estimate effort to design test cases (1-2 hours per test case typical for functional testing). Account for complexity: simple tests (e.g., valid input) take less time; complex tests (e.g., integration scenarios) take more. Include time for review and refinement.

3. **Estimate Test Execution**: Factor in execution time per test (typically faster if automated, slower if manual). For manual testing, estimate exploration time (10-20% of execution time). Include time for bug investigation, environment issues, and retesting. Add buffer for unexpected issues (10-15%).

4. **Estimate Automation Development**: If automating, estimate time to implement automation (typically 3-5x manual execution time initially). Account for framework setup, tool learning curve, maintenance. Leverage existing automation to reduce new automation effort.

5. **Validate with Historical Data**: Compare estimates to historical data from similar features. Adjust for team experience (new team members take longer; experienced team members faster). Update velocity/rate metrics after each cycle to improve future estimates.

## Anti-Patterns

- **Underestimating testing effort** — Guessing without considering all test types, edge cases, or team capacity leads to overcommitment and quality shortcuts. **Guard:** Use structured estimation approaches (bottom-up, checklist-based); compare to historical data; add contingency buffer (15-20%).

- **Ignoring automation maintenance** — Assuming automation eliminates ongoing effort ignores maintenance, flakiness, and tool management. **Guard:** Budget 20-30% for automation maintenance; include framework updates, test refactoring, flaky test fixes.

- **Static estimates across projects** — Using identical percentages (e.g., "testing is 30% of effort") ignores project variation. **Guard:** Adjust estimates based on scope, complexity, risk, team experience; track actual effort; refine estimates continuously.

## Further Reading

- _Software Estimation: Demystifying the Black Art_ by Steve McConnell — Comprehensive estimation techniques
- _Agile Estimation and Planning_ by Mike Cohn — Story point-based estimation

---
