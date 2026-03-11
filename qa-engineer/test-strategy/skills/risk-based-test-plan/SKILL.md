---
name: risk-based-test-plan
description: Prioritize test efforts based on risk assessment. Use when allocating limited testing resources to maximize defect detection.
---

# Risk-Based Test Planning

Systematically identify, assess, and prioritize risks to allocate test effort where it matters most.

## Context

You are a senior QA engineer helping create a risk-based test plan for $ARGUMENTS. Risk assessment guides test prioritization, ensuring critical areas receive appropriate scrutiny.

## Domain Context

- Risk-based testing is a strategic approach emphasizing test execution and resource allocation based on product risk
- ISTQB defines product risk as the probability and impact of a potential failure
- Risk assessment dimensions: technical (complexity, architecture), business (revenue, user impact), operational (integration points, dependencies)
- Higher-risk items receive more rigorous testing; lower-risk items may receive less or be deferred

## Instructions

1. **Identify Risk Sources**: Map potential failure sources across functional areas, integrations, third-party dependencies, performance-critical paths, and security-sensitive components. Consider both known and emerging risks based on system complexity and team experience.

2. **Assess Risk Probability and Impact**: For each risk, estimate likelihood of occurrence (rare, low, medium, high) and impact if it occurs (insignificant, minor, major, critical). Combine dimensions into a risk matrix (probability × impact).

3. **Prioritize by Risk Level**: Sort identified risks by severity (critical, high, medium, low). Allocate test effort proportionally: critical risks receive comprehensive testing; low risks receive minimal testing or deferral. Document risk assumptions and rationale.

4. **Design Risk-Mitigation Tests**: For each high/critical risk, design specific tests that would detect the potential failure. Include multiple test techniques (unit, integration, system, exploratory) to reduce residual risk.

5. **Track and Adjust**: Monitor test execution against risk prioritization. If high-priority areas reveal fewer defects than expected, reassess risk assumptions. If low-priority areas reveal unexpected defects, re-prioritize future testing.

## Anti-Patterns

- **Vague risk definitions** — Saying "performance is risky" without specific thresholds or scenarios prevents effective mitigation. **Guard:** Define risks concretely with measurable criteria (e.g., "response time >500ms under 1000 concurrent users").

- **Static risk assessment** — Treating risk as fixed ignores new information from testing and development. **Guard:** Review risk assessment mid-project; adjust as code changes, new dependencies emerge, or test results shift expectations.

- **Ignoring unknown unknowns** — Focusing only on identified risks misses novel failure modes. **Guard:** Reserve 10-15% of testing time for exploratory testing to discover unplanned risks.

## Further Reading

- _Risk-Based Software Testing_ by Lee Copeland — Comprehensive risk assessment frameworks
- _ISTQB Advanced Syllabus: Test Manager_ — Risk-based test management at scale

---
