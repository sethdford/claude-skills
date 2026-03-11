---
description: Run a cross-functional design review combining architecture, security, and UX perspectives.
argument-hint: "[feature or system to review]"
---

Conduct a comprehensive design review combining perspectives from architecture, security, and UX.

## Steps

1. **Architect System Decomposition** (`architect:system-decomposition`)
   - Input: Feature description or system boundary
   - Output: Component diagram, dependency list, scaling implications

2. **Security Threat Analysis** (`security:stride-analysis`)
   - Input: Architecture from step 1
   - Output: Threat model, attack vectors, required mitigations

3. **UX Accessibility Review** (`designer:accessibility-audit`)
   - Input: Design mockups or design spec
   - Output: Accessibility assessment (WCAG 2.1 compliance), interaction patterns

4. **Architect Trade-Off Analysis** (`architect:trade-off-analysis`)
   - Input: Concerns from security and UX reviews
   - Output: Documented trade-offs (performance vs. security, simplicity vs. flexibility)

5. **Synthesis**
   - Consolidate: Architecture + Threats + Accessibility + Trade-offs
   - Verdict: Approved / Conditional / Rejected with required changes
   - Risk Assessment: Severity and mitigation for remaining risks

## Output

**Design Review Report** containing:

- Approved design verdict
- Required changes (if conditional)
- Risk assessment with severity levels
- Remaining risks and their mitigations
- Recommendation: Ready for implementation or needs redesign

## Example
```

/sdlc:design-review "User authentication system redesign"

→ Architect decomposes: OAuth2 + JWT + session store
→ Security identifies: Token refresh strategy, session hijacking risks
→ Designer reviews: Login flow accessibility, mobile responsiveness
→ Architect documents: Security vs. complexity trade-offs
→ Synthesis: Approved with condition: "Session timeout must be ≤ 30 min"

Output: Design Review Report
Verdict: CONDITIONAL APPROVAL
Required Changes: Session timeout configuration
Risk Assessment: [table of risks, severity, mitigations]

```

## Next Steps

After design review approval, suggest:
- "Ready to move to `/sdlc:quality-gate` to verify the design meets phase gate criteria."
- "Create implementation tickets for any conditional changes."