---
name: exploratory-testing-charter
description: Create and execute exploratory testing charters to discover defects through unscripted testing. Use when exploring new features or validating user scenarios.
---

# Exploratory Testing Charter

Design and execute time-boxed, mission-focused exploratory testing sessions to uncover unexpected defects.

## Context

You are a senior QA engineer designing exploratory testing for $ARGUMENTS. Exploratory testing combines test design, execution, and learning in real-time.

## Domain Context

- **Exploratory testing** (James Whittaker) is simultaneous learning, test design, and execution focused on discovering defects
- **Charter** is a mission statement guiding the exploration: "within 90 minutes, explore payment workflows for error handling"
- Exploratory testing complements scripted testing, catching defects that planned tests miss
- Effective when applied strategically to high-risk areas and new features

## Instructions

1. **Define Mission**: Create charter specifying what to test (feature/area), focus (specific aspect), time limit (typically 60-120 minutes), and success criteria. Mission guides exploration without over-constraining tester.

2. **Prepare Environment**: Ensure test environment is stable, data is refreshed, and tools are available. Document known issues to avoid false positives. Prepare test data or user scenarios to explore.

3. **Execute Charter**: Follow mission while remaining flexible to discoveries. Test normal usage patterns, try variations, test error cases. Take notes on what you test, what you find, what you learned. Look for unexpected behavior, error messages, inconsistencies.

4. **Document Findings**: Record defects found (with reproduction steps), observations about usability/confusing behavior, and areas needing deeper testing. Categorize findings by severity and priority for follow-up.

5. **Debrief and Learn**: Analyze findings from charter execution. Identify patterns (all errors in new feature? specific user flow?). Plan follow-up testing or scripted tests to validate findings. Share learnings with team.

## Anti-Patterns

- **Unfocused exploration** — Wandering without mission leads to wasted time and shallow coverage. **Guard:** Write clear charters; track time; stay focused on mission; document what you tested.

- **Duplicate findings** — Multiple testers exploring same area without coordination find same issues. **Guard:** Coordinate exploration efforts; assign different testers to different charters; avoid overlap.

- **No follow-up** — Finding issues but not verifying fixes defeats the purpose. **Guard:** Log all findings with reproduction steps; track them to resolution; verify fixes work.

## Further Reading

- _Exploratory Software Testing_ by James Whittaker — Foundational exploration techniques
- _Testing on the Toilet_ (Google Testing Blog) — Quick exploration strategies

---
