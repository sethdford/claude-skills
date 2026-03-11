---
name: error-guessing
description: Experience-based testing technique that anticipates defects through intuition, domain knowledge, and common failure patterns. Use when supplementing systematic techniques with exploratory instinct.
---

# Error Guessing

Leverage testing experience and domain knowledge to anticipate where defects are most likely to hide, supplementing systematic test design with targeted intuition-driven tests.

## Context

You are a senior QA engineer applying error guessing to supplement systematic test design for $ARGUMENTS. This technique fills gaps that formal methods miss.

## Domain Context

- **ISTQB Advanced Test Analyst**: Classifies error guessing as an experience-based technique alongside exploratory testing and checklist-based testing (ISTQB-ATA 3.4)
- **Defect clustering**: Pareto principle applies — ~80% of defects concentrate in ~20% of modules (Myers, _The Art of Software Testing_)
- **Boris Beizer's bug taxonomy**: Common defect categories (boundary errors, off-by-one, null handling, race conditions, resource leaks) provide structured starting points
- **IEEE 829**: Test design documentation should capture the rationale behind experience-based test cases for repeatability

## Instructions

1. **Build a fault taxonomy**: Catalog common defect types relevant to the system under test — null/empty inputs, boundary values, type coercion errors, concurrency issues, encoding problems, timezone edge cases, permission escalation, and resource exhaustion
2. **Mine defect history**: Review past bug reports, production incidents, and hotfixes to identify recurring failure patterns specific to this codebase and team
3. **Map risk hotspots**: Identify areas with high complexity (cyclomatic complexity > 15), recent churn (many commits), new contributors, or tight deadlines — these correlate with higher defect density
4. **Design targeted tests**: For each anticipated defect, write a specific test case with:
   - The hypothesis (what could go wrong and why)
   - Input conditions that trigger the failure
   - Expected vs. actual behavior check
   - Severity if the defect exists
5. **Prioritize by impact**: Order error guesses by business impact x likelihood. Focus on scenarios where failure would cause data loss, security exposure, or user-facing errors
6. **Document and systematize**: Convert validated error guesses into regression tests. Build a team error checklist that grows over time.

## Anti-Patterns

- **Unstructured gut feeling** — LLMs generate vague "might fail" scenarios without specific inputs or expected outcomes. **Guard:** Every error guess must include a concrete test case with specific inputs and a verifiable assertion.
- **Recency bias in defect prediction** — LLMs over-weight recently discussed defect types and ignore domain-specific failure modes (e.g., suggesting SQL injection for an embedded system). **Guard:** Cross-reference guesses against the actual technology stack and defect history.
- **Ignoring the mundane** — LLMs gravitate toward exotic failure modes while missing common ones (empty strings, negative IDs, expired sessions, daylight saving transitions). **Guard:** Always cover the "boring" failure categories first — null, empty, boundary, permissions — before exploring edge cases.

## Further Reading

- Glenford Myers, _The Art of Software Testing_, 3rd Edition — Chapter 4 on error guessing as complement to systematic techniques
- Boris Beizer, _Software Testing Techniques_, 2nd Edition — Defect taxonomy and fault classification
- ISTQB Advanced Level Test Analyst Syllabus, Section 3.4 — Experience-based test techniques
- James Whittaker, _Exploratory Software Testing_ — Tours and attack models that structure error guessing

---
