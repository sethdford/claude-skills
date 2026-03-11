---
name: system-audit
description: Conduct comprehensive system architecture evaluation. Assess design quality, technical debt, operational readiness, scalability. Use when auditing existing systems.
---

# System Audit

Conduct comprehensive evaluation of system architecture and identify improvement opportunities.

## Context

You are auditing a system's architecture. Assess design quality, technical debt, operational readiness, scalability potential. Read code, infrastructure, metrics, team feedback.

## Domain Context

Based on architecture assessment frameworks:

- **Design Quality**: Modularity, coupling, cohesion. Is architecture aligned with business domains? Easy to change?
- **Operational Readiness**: Monitoring, alerting, logging, runbooks. Can ops team run this effectively? What happens when it fails?
- **Scalability**: Can it handle 10x growth? What's the bottleneck? Vertical or horizontal scaling?
- **Technical Debt**: What's slowing teams down? What would refactoring improve?
- **Security and Compliance**: Data protection, access control, audit trails, regulatory alignment?

## Instructions

1. **Prepare Audit Checklist**:
   - Architecture & Design (modularity, coupling, domain alignment)
   - Data (model, storage, flow, governance)
   - Scalability (bottlenecks, growth headroom)
   - Operations (monitoring, logging, alerting, runbooks)
   - Security & Compliance (data protection, access control, audit)
   - Team Productivity (deployment time, testing capability, cycle time)

2. **Gather Information**:
   - Read architecture documentation, design documents
   - Review code structure, dependencies
   - Check infrastructure-as-code, deployment pipelines
   - Interview team: "What's hard? What's slow? What worries you?"
   - Review metrics: latency, error rate, utilization, deployment frequency

3. **Assess Each Area**:
   - Score: Good (no action needed), Fair (monitor, improve over time), Poor (urgent)
   - Document evidence: "Monolith 500K lines, 30-min builds, hard to test"

4. **Identify Patterns**:
   - Common themes? Multiple "poor" scores suggest systemic issues.
   - Root causes: "Tight coupling causing hard deployments and scaling issues"

5. **Recommend Improvements**:
   - Prioritize by impact and effort
   - Quick wins (low effort, high impact): improve monitoring, document runbooks
   - Strategic initiatives (high effort, high impact): decompose monolith, refactor critical paths
   - Timeline: what's urgent vs 2-year plan?

6. **Document and Present**:
   - Written report with findings and recommendations
   - Present to leadership and team
   - Create roadmap for improvements
   - Follow up in 6 months to measure progress

## Anti-Patterns

- **Audit Without Action**: Produce report, file it away. Result: wasted effort, team cynicism. **Guard**: Use audit to drive improvements; track follow-up.
- **Oversimplified Scoring**: Everything is "good" or "poor" with no nuance. Result: not actionable. **Guard**: Explain context; acknowledge tradeoffs; show path forward.
- **Ignoring Team Input**: Audit from outside perspective only. Result: miss what team actually struggles with. **Guard**: Interview team; their perspective is crucial.
- **Unrealistic Recommendations**: Suggest complete rewrite. Result: ignored, too ambitious. **Guard**: Suggest achievable improvements; prioritize by ROI.

## Further Reading

- _Software Architecture in Practice_ by Len Bass et al. — architecture evaluation methods
- _Assessing Organizational Alignment_ — evaluating organizational health
- _Technical Debt Management_ — evaluating debt and improvement priorities
