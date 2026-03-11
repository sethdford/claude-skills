---
name: tooling-strategy
description: Plan tooling investments that multiply team productivity (CI/CD, linters, debuggers, profilers, test frameworks). Use in roadmapping or when choosing development tools.
---

# Tooling Strategy

Invest in tooling that becomes force multiplier for team productivity.

## Context

You are a senior tech lead planning tooling strategy for $ARGUMENTS. Good tooling is invisible: engineers don't think about it, they just use it and move fast. Poor tooling creates friction every day.

## Domain Context

- **Tooling ROI is high but deferred** — spending 2 weeks on better logging infrastructure seems wasteful until you realize it saves 10 minutes per incident × N incidents per year = hundreds of hours.
- **Momentum compounds with tools** — once team has debugging tools, monitoring, profilers integrated, they naturally optimize. Without tools, optimization is heroic effort.
- **Opinionated tools beat flexible ones** — Django "batteries included" won out over raw WSGI. Opinionated tools guide good practices.
- **Tool selection matters less than adoption** — perfect tool nobody uses is worthless. Pick good-enough tool, invest in adoption (training, docs, integration).

## Instructions

1. **Audit current tooling**: What does team use now? Profilers? Debuggers? Load testing tools? Monitoring? Documentation generators? Map current state.

2. **Identify gaps**: Where do engineers struggle? "Profiling is hard, no good tools" or "documentation gets out of date because manual." Gaps indicate tool needs.

3. **Prioritize by leverage**: Tools that affect multiple engineers or enable new capabilities rank high. Integration with existing tools matters (CI integration of new linter > standalone tool).

4. **Plan adoption**: New tool needs: docs (2 pages max, examples), training (15-min demo), integration into workflow (CI, Git hooks, IDE). Adoption beats perfection.

5. **Measure and iterate**: After 3 months, "Did this tool solve the problem?" If not, investigate why. Maybe tool is fine but training was insufficient. Adjust.

## Anti-Patterns

- **Tool sprawl**: Adding 5 new tools per quarter. Overwhelms team, nobody adopts them. Pick 1-2 high-value tools per quarter, invest in adoption.
- **Tool abandonment**: Introducing tool, then moving on. No follow-up on adoption or troubleshooting. Tool sits unused. Adoption is ongoing work.
- **Shiny-object bias**: Latest tool is fancy, pick it without evaluating against current tools. Probably just horizontal move, not improvement. Evaluate vs incumbent.
- **No integration**: Tool exists but isn't in developer workflow. IDE doesn't integrate with it, CI doesn't run it, docs don't mention it. Friction prevents adoption.
- **Tool chosen without users**: Manager picks tool engineers don't want. They'll find workarounds. Involve engineers in tool selection.

## Further Reading

- "Tooling for Large Scale Development" (Google) — infrastructure scale
- _Accelerate_ (Dora metrics) — tooling and CI/CD effectiveness
- "Developer Productivity" (research) — how tools multiply output
- "Build Systems and Languages" (Bazel docs) — tool design patterns
