# Definition of Done

Validates completed work across all dimensions: code quality, test coverage, security review, documentation, accessibility. This is the intersection of all roles' acceptance criteria.

## Domain Context

**Definition of Done** (DoD) is the collective agreement about what "complete" means. Without it, developers ship code they think is done, QA finds problems, and conflicts arise over who's responsible.

The critical insight: **DoD is not just about code quality.** It's about:

- **Engineer** — Code follows standards, unit tests pass, no obvious bugs
- **QA** — Feature works as designed, test coverage is adequate, edge cases pass
- **Security** — No known vulnerabilities, secrets are not committed, OWASP risks mitigated
- **Designer** — Matches design spec, accessibility standards met, responsive on target devices
- **Tech Lead** — Documentation is written, team can maintain this, deployment is safe

A feature is "done" when all five perspectives agree it's production-ready.

**ISO/IEC 12207 Reference:**

- 5.3.6 Implementation (code review, unit testing)
- 5.3.7 Integration (integration testing)
- 5.3.8 Verification (acceptance testing)
- 5.3.9 Transition (deployment readiness)

## Instructions

### Step 1: Engineer Perspective — Code Quality

Check:

- **Code Review**: Has the code been reviewed by at least one other engineer?
- **Standards**: Does it follow the team's code style, naming conventions, patterns?
- **Linting**: Do static analysis tools pass? (no warnings, no complexity violations)
- **Unit Tests**: Are unit tests written? Do they pass? Coverage >= threshold?
- **No Obvious Bugs**: Does the implementation match the design? Are error cases handled?
- **Refactoring Debt**: Is the code ready for production, or does it need cleanup?
- **Comments/Clarity**: Is the code readable? Are complex sections documented?

Output: Code quality checklist

### Step 2: QA Perspective — Test Coverage and Functionality

Check:

- **Functional Testing**: Does the feature work as designed in the acceptance criteria?
- **Edge Cases**: Have edge cases been tested? (empty inputs, boundary conditions, race conditions)
- **Error Cases**: Does the system gracefully handle errors? (network failures, invalid data, timeouts)
- **Integration Testing**: Does this integrate correctly with other systems?
- **Regression Testing**: Did this break anything else? (related features, adjacent code paths)
- **Test Coverage**: Is the coverage above the team's threshold?
- **Test Documentation**: Are tests clear enough for others to maintain them?

Output: Test coverage checklist

### Step 3: Security Perspective — Vulnerability Scanning and Review

Check:

- **Secrets Scan**: No API keys, passwords, or credentials in code/logs?
- **Dependency Audit**: Any high or critical CVEs in dependencies?
- **SAST Scan**: Static analysis found no security issues? (SQL injection, XSS, CSRF, etc.)
- **DAST Scope**: For APIs/web features: scanning queued or completed?
- **Access Control**: Are permissions correctly enforced? Is data properly isolated?
- **Data Handling**: PII/sensitive data encrypted at rest and in transit?
- **Security Review**: Has security team reviewed the implementation?

Output: Security checklist

### Step 4: Designer Perspective — Design Fidelity and Accessibility

Check:

- **Visual Design**: Does the UI match the design specification?
- **Responsive**: Does it work on target devices/screen sizes?
- **Interactions**: Do animations, transitions, and interactions match the design?
- **Accessibility**:
  - WCAG 2.1 AA compliant (color contrast, font sizes, focus states)?
  - Screen reader compatible?
  - Keyboard navigable?
  - Reduced motion respected?
- **Content**: Copy/microcopy matches approved content?
- **Internationalization**: If multi-language, is text extracted and localized correctly?

Output: Design and accessibility checklist

### Step 5: Tech Lead Perspective — Documentation, Maintainability, Deployment

Check:

- **Code Documentation**: Modules, complex functions documented? README updated?
- **API Documentation**: If this exposes an API, is it documented?
- **Runbook**: For ops-sensitive changes, is a runbook written?
- **Team Knowledge**: Can another team member understand and maintain this?
- **Deployment Safety**: Is there a rollback procedure? Are deployment steps documented?
- **Performance**: Have baselines been captured? Will this regress performance?
- **Monitoring**: Are the right metrics/logs instrumented to monitor in production?
- **Release Notes**: Is the feature described for release communications?

Output: Documentation and deployment checklist

### Step 6: Consolidate the DoD Checklist
```

DoD Checklist for [Feature/PR]: [Title]

[ ] Engineer
[ ] Code reviewed (at least 1 reviewer)
[ ] Follows team standards and conventions
[ ] Linting and static analysis passing
[ ] Unit tests written and passing
[ ] Coverage >= [threshold]%
[ ] No obvious bugs; error cases handled
[ ] Code is clear and documented

[ ] QA
[ ] Feature works as per acceptance criteria
[ ] Edge cases tested and passing
[ ] Error cases tested
[ ] Integration testing complete
[ ] Regression testing shows no breaks
[ ] Test coverage adequate
[ ] Tests are maintainable and clear

[ ] Security
[ ] Secrets scan passed (no credentials in code)
[ ] Dependency audit passed (no high/critical CVEs)
[ ] SAST scan passed
[ ] DAST scan queued or completed
[ ] Access control correctly enforced
[ ] Data sensitivity handled properly
[ ] Security team reviewed

[ ] Designer
[ ] UI matches design specification
[ ] Responsive on all target devices
[ ] Interactions match design
[ ] WCAG 2.1 AA compliance verified
[ ] Screen reader tested
[ ] Keyboard navigable
[ ] Copy/content approved

[ ] Tech Lead
[ ] Code documented (README, inline comments)
[ ] API documented (if applicable)
[ ] Runbook written (if ops-sensitive)
[ ] Maintainability verified
[ ] Deployment strategy documented
[ ] Rollback procedure documented
[ ] Monitoring/logging configured
[ ] Performance baseline captured
[ ] Release notes prepared

Done? [ ] Yes (all boxes checked) [ ] No (see blocking issues below)

```

### Step 7: Identify Failing Criteria

For each unchecked box:
- **What failed?** (specific failing test, code review comment, security issue)
- **Who fixes it?** (engineer, QA, security, designer, tech lead)
- **How long?** (estimate in hours)
- **Blocks deployment?** (critical, high, medium, low priority)

Critical/high issues block production deployment.

### Step 8: Make the Done/Not Done Decision

**Done Decision:**
- All boxes are checked
- No critical issues remain
- Document: "Feature is done and approved for deployment. Sign-offs: [engineer], [QA], [security], [designer], [tech lead]."

**Not Done Decision:**
- Critical issues remain
- Document: "Feature is not done. Blocker issues: [list]. Required fixes: [list]. Estimated re-check: [date/time]."

## Anti-Patterns

1. **DoD that's too strict**
   - Mistake: "Every feature must have 90%+ coverage and 100% documentation"
   - Correct: DoD should reflect team risk tolerance and product maturity
   - Fix: Adjust DoD based on team data; don't optimize away shipping

2. **DoD that's only about code**
   - Mistake: "DoD is just linting, tests, and code review"
   - Correct: DoD includes security, design, ops, and documentation
   - Fix: Require sign-off from QA, security, and designer; not just engineers

3. **Skipping the security review because "it's low-risk"**
   - Mistake: "This is just adding a button; security review not needed"
   - Correct: Every feature should pass the same DoD bar
   - Fix: Empower security to do fast sign-off for low-risk items

4. **DoD that changes per sprint**
   - Mistake: "This week we're busy, so let's relax DoD"
   - Correct: DoD should be stable; if you're too busy, the sprint is too big
   - Fix: Protect DoD; adjust sprint scope instead

5. **Using DoD to avoid accountability**
   - Mistake: "DoD says tests must pass, but we shipped without running them"
   - Correct: DoD requires verification, not just paperwork
   - Fix: Automate DoD checks (CI/CD pipelines); require explicit sign-off

6. **Not evolving DoD based on incidents**
   - Mistake: "A security bug shipped because DoD didn't catch it, but we don't update DoD"
   - Correct: Every production incident should trigger a DoD improvement
   - Fix: Retro question: "Does this incident suggest a DoD change?"

## Further Reading

- **Scrum Guide** — Schwaber, K. & Sutherland, J., Definition of Done (https://scrumguides.org/)
- **Continuous Delivery** — Humble, J. & Farley, D., "Continuous Delivery: Reliable Software Releases through Build, Test, and Deployment Automation" (Addison-Wesley)
- **Quality Standards** — ISO/IEC 9126, Software Product Quality