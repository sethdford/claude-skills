---
description: Launch a feature with full cross-functional alignment and DoR validation.
argument-hint: "[feature name or epic name]"
---

Conduct a feature kickoff that aligns all teams and validates Definition of Ready.

## Steps

1. **PM Problem Statement** (`product-manager:problem-statement`)
   - Input: Feature request or roadmap item
   - Output: Problem statement, success metrics, user impact

2. **PM PRD Template** (`product-manager:prd-template`)
   - Input: Problem statement
   - Output: Product requirements document (user stories, acceptance criteria, constraints)

3. **Architect System Decomposition** (`architect:system-decomposition`)
   - Input: Requirements from PRD
   - Output: Component diagram, complexity assessment, feasibility

4. **Security Threat Analysis** (`security:stride-analysis`)
   - Input: System decomposition
   - Output: Threat model, required security controls

5. **Tech Lead Work Breakdown** (`tech-lead:work-breakdown-structure`)
   - Input: Requirements + Threats + Architecture
   - Output: Work breakdown structure with effort estimates

6. **Definition of Ready Validation** (`sdlc:definition-of-ready`)
   - Input: All artifacts from above
   - Output: DoR checklist with approval

## Output

**Kickoff Summary** containing:

- Aligned team understanding of the problem
- Acceptance criteria everyone agrees on
- Architecture that the team commits to
- Security assumptions and requirements
- Work breakdown with effort estimates
- Definition of Ready checklist

## Example
```

/sdlc:feature-kickoff "Multi-factor authentication"

→ PM articulates: "Users need MFA to reduce account takeovers"
→ PRD defines: Support SMS + TOTP, allow user to disable, fallback via email
→ Architect proposes: Service + factor provider abstraction
→ Security identifies: Session invalidation on MFA setup, rate limiting, backup codes
→ Tech Lead estimates: 8 days (architect), 16 days (backend), 10 days (frontend), 5 days (QA), 2 days (security)
→ DoR validates: All criteria met

Output: Kickoff Summary
Problem: Reduce account takeovers via MFA
Success Metric: 80% user adoption within 3 months
Architecture: Service + provider abstraction
Security Assumptions: [list]
Work Breakdown: [timeline]
DoR Status: APPROVED

```

## Next Steps

- "Feature is ready for sprint planning. Add all work breakdown items to the backlog."
- "Schedule architecture review before development starts."