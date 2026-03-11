---
description: Comprehensive pre-release validation across all roles.
argument-hint: "[feature set or release version]"
---

Run a full pre-release validation across PM, QA, security, and operations.

## Steps

1. **Release Checklist** (`sdlc:release-checklist`)
   - Input: Feature set, release notes, deployment plan
   - Output: Release readiness checklist

2. **Engineer Deployment Strategy** (`engineer:deployment-strategy`)
   - Input: Features to deploy
   - Output: Deployment plan, rollback procedure, risk assessment

3. **Security Penetration Test Scope** (`security:penetration-test-scope`)
   - Input: Features to deploy
   - Output: Pen testing plan, scope, success criteria

4. **QA Release Readiness** (`qa:release-readiness-assessment`)
   - Input: Features, test results, known issues
   - Output: Test completion status, risk assessment

5. **PM Launch Readiness** (`product-manager:launch-readiness-checklist`)
   - Input: Features, success metrics, communications
   - Output: Launch readiness, customer communications, stakeholder approval

## Output

**Pre-Launch Report** containing:

- Release readiness matrix (PM, QA, security, engineer, tech lead sign-offs)
- Test completion and coverage
- Known issues and severity assessment
- Deployment and rollback procedures
- Launch communication plan
- Blocking issues (if any)

## Example
```

/sdlc:pre-launch-review "Payment redesign v2.0"

→ Release Checklist: 95% pass (1 warning on performance)
→ Deployment Strategy: Blue-green with 15-minute cutover
→ Security Pen Test: Scope approved, scheduled for tomorrow
→ QA: All test cases passing, 98% coverage, 3 known low-severity bugs
→ PM: Launch communication ready, stakeholder approval obtained

Output: Pre-Launch Report
Release Ready: YES (subject to pen test completion)
Test Coverage: 98%
Blocking Issues: None
Warnings: Performance testing shows 5% regression under load
Sign-offs: [PM ✓] [Engineer ✓] [QA ✓] [Security ⏳] [Tech Lead ✓]

```

## Next Steps

- "Pen test results received, approve or address findings."
- "Ready to deploy to production." OR "Address warnings before deploying."