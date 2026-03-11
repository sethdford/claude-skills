---
description: Validate work meets all quality standards before advancement.
argument-hint: "[feature name or work item]"
---

Run a comprehensive quality gate that validates work across code quality, test coverage, security, and operations readiness.

## Steps

1. **SDLC Phase Gate** (`sdlc:sdlc-phase-gate`)
   - Input: Current work phase, work item
   - Output: Phase gate decision (go/conditional/no-go)

2. **Definition of Done** (`sdlc:definition-of-done`)
   - Input: Completed work
   - Output: DoD checklist with role sign-offs

3. **QA Test Coverage Analysis** (`qa:test-coverage-analysis`)
   - Input: Code and test results
   - Output: Coverage report, gap analysis

4. **Engineer Code Complexity** (`engineer:code-complexity-analysis`)
   - Input: Code changes
   - Output: Complexity assessment, refactoring recommendations

5. **Security Scan** (`security:security-scan`)
   - Input: Code and dependencies
   - Output: Vulnerability report, remediation plan

## Output

**Quality Gate Report** containing:

- Phase gate verdict
- DoD checklist status
- Test coverage analysis
- Code complexity assessment
- Security scan results
- Overall go/no-go decision with blocking issues

## Example
```

/sdlc:quality-gate "Search filtering feature"

→ Phase Gate: Ready to move from Development to Testing
→ DoD: 8/10 criteria met (missing performance baseline, accessibility test)
→ Test Coverage: 92% (above 85% threshold)
→ Code Complexity: Cyclomatic complexity 8 (acceptable)
→ Security Scan: 0 critical, 2 medium (remediation plan in progress)

Output: Quality Gate Report
Phase Gate: CONDITIONAL (requires DoD completion)
Test Coverage: PASS (92%)
Code Complexity: PASS
Security: CONDITIONAL (address 2 medium issues)
Overall: NOT READY — Complete DoD and security remediation
Blocking Issues: [list]

```

## Next Steps

- "Fix DoD gaps (performance baseline, accessibility test)."
- "Address security medium-risk issues."
- "Re-run quality gate when complete."