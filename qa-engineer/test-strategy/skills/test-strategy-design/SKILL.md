---
name: test-strategy-design
description: Design comprehensive test strategies aligned with project goals, risks, and constraints. Use when planning testing efforts for new projects or major releases.
---

# Test Strategy Design

Create a cohesive, risk-aligned testing strategy that balances quality goals, resource constraints, and delivery timelines.

## Context

You are a senior QA engineer helping design a test strategy for $ARGUMENTS. This strategy should be documented, stakeholder-aligned, and achievable within project constraints.

## Domain Context

- **ISTQB Foundation Syllabus** defines test strategy as a high-level document describing the testing approach, scope, and timing
- Test strategy differs from test plan (strategic vs. tactical) and differs from test approach (positioning vs. organization)
- Effective strategies balance coverage (what to test), technique (how to test), and cost (resources and time)
- Risk-based testing prioritizes test effort on higher-risk areas to maximize defect detection per unit of effort

## Instructions

1. **Understand Project Context**: Review project goals, technology stack, team skills, timeline, and quality expectations. Identify stakeholder concerns and regulatory requirements (if any). This forms the foundation for strategy decisions.

2. **Identify Testing Scope**: Determine what will be tested (features, integrations, performance, security) and what explicitly won't be tested (out-of-scope). Define scope boundaries to prevent scope creep and misaligned expectations.

3. **Map Risks and Priorities**: Conduct risk assessment across functional, technical, and business dimensions. Prioritize areas requiring deeper testing (high-risk, high-visibility, high-impact features). Document risk assumptions.

4. **Design Test Levels and Balance**: Decide the distribution across unit testing (developer-owned), integration testing (component interactions), system testing (end-to-end), and acceptance testing (business validation). Align with the test pyramid principle (70% unit, 20% integration, 10% E2E).

5. **Document Testing Approach**: Specify test techniques (manual, automated, exploratory), test types (functional, performance, security, accessibility), and test data strategy. Detail entry/exit criteria for each test level. Document assumptions, dependencies, and resource needs.

## Anti-Patterns

- **Lack of risk prioritization** — Testing everything equally wastes effort on low-risk areas while missing high-risk defects. **Guard:** Always conduct risk assessment first; allocate test effort proportionally to risk levels.

- **Overcommitting automation** — Assuming all tests can be automated ignores maintenance costs and execution time. **Guard:** Reserve 20-30% of test effort for exploratory and manual testing; automate stable, repeatable scenarios only.

- **Missing stakeholder alignment** — A strategy created in isolation fails when stakeholders expect different coverage or quality levels. **Guard:** Present the strategy to product, engineering, and business stakeholders; iterate based on feedback before committing resources.

## Further Reading

- _ISTQB Foundation Syllabus_ — Test strategy and planning foundations
- _Risk-Based Software Testing_ by Lee Copeland — Strategic risk prioritization
- _Agile Testing_ by Lisa Crispin & Janet Gregory — Agile test strategy patterns

---
