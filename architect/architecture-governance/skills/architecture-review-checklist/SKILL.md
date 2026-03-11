---
name: architecture-review-checklist
description: Standardized architecture review process with consistent criteria. Evaluate systems against principles, quality attributes, and operational readiness. Use when conducting architecture reviews.
---

# Architecture Review Checklist

Establish standardized architecture review process with clear criteria and repeatable outcomes.

## Context

You are conducting architecture reviews. Evaluate designs against principles, quality attributes, operational readiness. Use consistent checklist; document decisions and rationale.

## Domain Context

Based on architecture review frameworks and governance:

- **Design Review**: Does proposed design align with principles? Are quality attributes met? Trade-offs understood?
- **Operational Readiness**: Monitoring, alerting, logging, runbooks documented? Disaster recovery plan? Capacity forecast?
- **Security Review**: Authentication, authorization, secrets management, data protection? Compliance with regulations?
- **Cost Impact**: Infrastructure cost projections? Optimizations considered? Budget alignment?

## Instructions

1. **Prepare Checklist**:
   - Alignment: Does design follow architecture principles?
   - Quality Attributes: Addresses scalability, reliability, security, maintainability?
   - Dependencies: External services, databases, message queues? All documented?
   - Operations: Monitoring, alerting, logging, runbooks? On-call procedure?
   - Testing: Unit tests, integration tests, chaos testing? Coverage adequate?
   - Compliance: GDPR, CCPA, HIPAA? Data residency requirements met?
   - Cost: Projected monthly cost? Optimization opportunities?

2. **Conduct Review**: Present architecture. Walk through checklist. Score each item: met, partially met, not met. Discuss gaps and remediation.

3. **Document Decision**: Record what's approved, what needs work, contingencies. Link to design document. Assign owners for open items.

4. **Track Follow-Up**: Monitor that remediation happens before deployment. Close items only after verification.

5. **Iterate**: If review uncovers major issues, schedule follow-up review. Use past reviews to improve checklist.

## Anti-Patterns

- **Reviews Without Teeth**: Checklist completed, issues noted, nothing changes. Result: wastes time. **Guard**: Reviews block deployment; open items must be resolved or documented as accepted risk.
- **Checklist Without Context**: Rote questions without understanding trade-offs. Result: surface-level feedback. **Guard**: Reviewer understands domain; asks "why?" on answers.
- **No Documentation**: Verbal feedback, forgotten after meeting. Result: team doesn't know what was approved. **Guard**: Written decision with rationale; link to design docs.
- **Infrequent Reviews**: Only at major milestones. Result: missed issues accumulate. **Guard**: Reviews on feature gates, before production, monthly architecture sync.

## Further Reading

- _Software Architecture in Practice_ by Len Bass et al. — architecture review processes
- _Architectural Thinking_ by Nathaniel Schutta — critical evaluation skills
- _Software Architecture Fundamentals_ by Mark Richards — review and governance
