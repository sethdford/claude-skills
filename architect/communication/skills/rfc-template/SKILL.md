---
name: rfc-template
description: Propose architectural changes with comprehensive RFCs. Structure feedback, document decisions, track rationale. Use when proposing major architecture changes or design patterns.
---

# RFC Template

Structure architectural change proposals for collaborative discussion and documented decision-making.

## Context

You are proposing a major architectural change. Use RFC (Request for Comments) format to solicit feedback, document rationale, and create audit trail. Read existing architecture, team concerns, and alternatives.

## Domain Context

Based on RFC processes (Rust RFCs, Internet RFCs):

- **Problem Statement**: What's broken? Why change? Quantify impact (latency, cost, developer productivity).
- **Proposed Solution**: How does RFC solve problem? What's the mechanism?
- **Detailed Design**: Implementation details. APIs, data structures, state management. Enough to review feasibility.
- **Alternatives Considered**: What else did you think about? Why choose this one?
- **Drawbacks and Risks**: What could go wrong? Performance impact? Operational complexity? Compatibility issues?

## Instructions

1. **RFC Header**:
   - Title: "Migrate from Monolith to Microservices"
   - Status: Draft/Discussion/Approved/Implemented
   - Author(s)
   - Date
   - Related Issues/PRs

2. **Problem Section**:
   - Current state: Monolithic Node.js app, 500K LOC, hard to test, deploy, scale
   - Pain points: 20-minute builds, deployments block all teams, scaling one service scales everything
   - Impact: 2 hours/week lost to build/deploy, 1 outage/quarter from scaling issues

3. **Proposed Solution**:
   - Split into services: API Gateway, Auth, Payment, Orders, Notifications
   - Each service: independent repo, CI/CD, database, deployment
   - Communication: REST APIs, async via RabbitMQ for events

4. **Design Details**:
   - Service boundaries (business domain alignment)
   - API contracts (OpenAPI specs)
   - Data consistency model (eventual consistency between services)
   - Deployment strategy (phased, start with payment service)

5. **Alternatives**:
   - Monolith + horizontal scaling: Cheaper short-term, doesn't solve coupling
   - Plugins/modular monolith: Simpler than microservices, still shared deployment

## Anti-Patterns

- **RFC Too Late**: Propose RFC after implementation started. Result: feedback ignored, decision already made. **Guard**: RFC before coding; treat as discussion forum.
- **Vague Proposal**: "Move to microservices" without design. Result: unclear feasibility. **Guard**: Enough detail to assess technical viability.
- **Ignoring Feedback**: RFC approved but objections recorded. Result: resentment, sabotage. **Guard**: Address all concerns; if not addressed, document why; build consensus.
- **No Implementation Plan**: Approve RFC, then surprise team with work. Result: chaos. **Guard**: RFC includes timeline, resource allocation, rollback plan.

## Further Reading

- _Rust RFC Process_ — open RFC governance model
- _Architecture Decision Records_ by Michael Nygard — lightweight decision documentation
- _Communicating Design_ by Dan Brown — presenting proposals effectively
