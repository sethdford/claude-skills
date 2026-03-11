---
name: development-workflow
description: Design development workflows that balance speed, quality, and safety. Use when establishing team processes or improving delivery efficiency.
---

# Development Workflow

Build processes that move code from idea to production reliably while preventing bottlenecks that slow shipping.

## Context

You are a senior tech lead designing development workflows for $ARGUMENTS. Process either accelerates or strangles delivery. Good workflows make quality the default, not an afterthought.

## Domain Context

- **Development workflow is inventory management** — work in progress (WIP) that sits between dev and production ties up engineering effort. Lower WIP = faster flow.
- **Feedback loops compound quality** — catching issues early (in PR, not production) is 10x cheaper than production firefighting. Build short feedback loops.
- **Process fatigue kills quality** — 15-step approval process that takes 3 weeks doesn't improve quality, it motivates engineers to cut corners. Simple processes that move fast win.
- **Friction accumulates** — one 30-minute approval delay × 10 PRs per week × 52 weeks = 260 hours lost per engineer per year. Small frictions compound massively.

## Instructions

1. **Map current workflow**: Draw the actual flow from "idea" to "in production". Include code review, testing, deployment approvals, documentation. How long does a typical PR take? Where does it get stuck?

2. **Identify bottlenecks**: Where do PRs wait? Code review queue? Deployment approval? Manual testing? Prioritize fixing the constraint (the step that determines overall throughput, not just delay).

3. **Design with constraints in mind**: Can you add parallel steps? "Code review and automated testing happen in parallel" is faster than "test after review." Can you reduce review scope (shorter PRs)? Can you automate approval (policy-based gates instead of humans)?

4. **Set targets**: Median PR time from open to merge: target 24 hours. 95%ile PR time: target 48 hours. Too-long outliers indicate broken process. Track metrics and investigate.

5. **Iterate based on data**: Workflow won't be perfect initially. Measure bottlenecks (time spent waiting vs time spent working). Adjust. Ideal target: 70% time working, 30% time waiting. If it's inverted, process is broken.

## Anti-Patterns

- **Process for its own sake**: Adding gates because "we should have higher quality" without data. If code review catches 2 bugs per 100 PRs but takes 2 hours per PR, that gate might hurt more than help. Measure.
- **Optimization for rare cases**: "We had one incident caused by missing docs, so now all PRs need extensive documentation." Rare incidents drive disproportionate process. Triage: common issues drive process, rare ones drive monitoring.
- **Serial dependencies**: "Dev can't start until design approves" locks up teams. Parallel workflows move faster. Design review happens alongside dev, not before it starts.
- **Gatekeeping as quality assurance**: Slow approval doesn't improve code, it just delays shipping. Quality comes from testing, code review clarity, and monitoring, not approval speed.
- **No escape valves**: 100% process adherence for emergencies kills response time. Hotfix process should bypass normal approval (with documentation after-the-fact). Have different processes for different risk levels.

## Further Reading

- _The Phoenix Project_ (Gene Kim) — workflow and bottleneck management
- _Accelerate_ (Dora metrics) — deployment frequency and process efficiency
- _Flow_ (Csikszentmihalyi) — how process affects human performance
- "Continuous Delivery" (Humble & Farley) — pipeline architecture for speed
