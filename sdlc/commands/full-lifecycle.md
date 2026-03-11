---
description: Trace a feature from problem statement through post-deployment monitoring.
argument-hint: "[feature name or epic name]"
---

Map a feature's complete lifecycle from problem definition through production stability.

## Steps

1. **PM Problem Statement** (`product-manager:problem-statement`)
   - Output: Problem, success metrics

2. **Architect System Decomposition** (`architect:system-decomposition`)
   - Output: Architecture, components, scaling plan

3. **Definition of Ready** (`sdlc:definition-of-ready`)
   - Output: DoR validation

4. **Engineer Test Strategy** (`engineer:test-strategy`)
   - Output: Unit, integration, and system test plans

5. **Security Threat Analysis** (`security:stride-analysis`)
   - Output: Threat model, required controls

6. **QA Test Strategy** (`qa:test-strategy-design`)
   - Output: QA test cases, coverage plan

7. **Definition of Done** (`sdlc:definition-of-done`)
   - Output: DoD validation

8. **Release Checklist** (`sdlc:release-checklist`)
   - Output: Pre-deployment validation

## Output

**Feature Lifecycle Document** containing:

- Requirements → Design → Implementation → Testing → Deployment → Operations timeline
- Linked artifacts at each phase (PRD, architecture, code, tests, deployment plan)
- Role contributions and sign-offs
- Metrics and monitoring strategy
- Post-launch actions and follow-ups

## Example
```

/sdlc:full-lifecycle "Dark mode support"

→ PM: "Reduce eye strain for evening users" (success: 40% adoption in 1 month)
→ Architect: CSS custom properties + system preference detection + storage
→ DoR: Requirements, design, feasibility approved
→ Engineer: Unit tests for preference logic, system tests for UI
→ Security: No threats identified, no auth changes
→ QA: Visual regression tests on 5 target devices
→ DoD: All tests passing, accessibility verified, docs updated
→ Release: Deployment to 10% users, monitor for CSS issues

Output: Feature Lifecycle Document
[Timeline from problem → production]
[Linked artifacts]
[Role contributions]
[Monitoring dashboard links]

```

## Next Steps

- "Feature is ready for next phase: [Design / Development / Testing / Deployment / Operations]."
- "Review lifecycle document with team; update as you progress."