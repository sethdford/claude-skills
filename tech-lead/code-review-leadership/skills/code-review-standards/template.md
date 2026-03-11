# Code Review Standards Template

## Scope

**What requires code review:**

- [ ] All production code changes
- [ ] Configuration files
- [ ] Test files and test infrastructure
- [ ] Infrastructure and deployment code
- [ ] Documentation (docs, README, comments)
- [ ] Dependency additions/updates

**Fast-track exceptions** (lighter review):

- [ ] Single-line typo fixes
- [ ] Documentation-only corrections
- [ ] Reverts of broken code
- [ ] Emergency hotfixes during outage (post-mortem review within 24h)

---

## Acceptance Checklist (Blocking Items)

Code must meet ALL of these before approval:

- [ ] **Compiles/runs without errors**: Code builds successfully; all tests pass
- [ ] **Tests included for new logic**: Minimum coverage (happy path + 1 error case)
- [ ] **No obvious performance regressions**: No O(n²) where O(n) is reasonable
- [ ] **Error handling present**: Exceptions caught and handled appropriately
- [ ] **Security review passed**: If code touches auth, payments, or data access
- [ ] **Documentation updated**: Code comments, README, API docs if applicable
- [ ] **Follows style guide**: [Link to style guide]; enforced by linter where possible
- [ ] **Minimal complexity increase**: No unnecessary abstractions; KISS principle

---

## Nits vs. Blockers

### Nits (Request Only, Not Blocking)

These are suggestions, not requirements. Author can choose to address or explain why they chose not to.

- [ ] Style/formatting (should be auto-enforced by linter/formatter)
- [ ] Naming preferences (code is clear; author's naming is reasonable)
- [ ] Code comment suggestions (code is self-documenting; comment would be nice)
- [ ] Unused imports/variables
- [ ] Log verbosity (does it log too much?)

**Comment format for nits**: _"Nit: Consider naming this..."_ or _"Nice to have:..."_

### Blockers (Must Fix)

These must be addressed before merge. Author and reviewer discuss if unclear.

- [ ] Logic bugs (code doesn't do what PR claims)
- [ ] Missing tests (new behavior without test coverage)
- [ ] Security vulnerabilities (injection, auth bypass, exposed secrets)
- [ ] Architectural violations (violates system design or technical strategy)
- [ ] Performance regression (measurable slowdown on critical path)
- [ ] Missing error handling (unhandled exception could crash service)

**Comment format for blockers**: _"Blocker: This needs to be fixed..."_

---

## Timing & Process

- **Review target**: [4-8 business hours from PR submission]
- **Approval target**: [8 business hours; if no response, author can merge with second reviewer]
- **Review rounds**: One round typical for trivial fixes; re-review required after blocker fixes

**Escalation**:

- Disagreement on code design → Tech lead as tiebreaker (30-min sync)
- Reviewer blocking unreasonably → Tech lead intervenes

---

## Approvers

- **Any [senior engineer / tech lead]** can approve [most PRs]
- **Specific roles** must approve: [Database schema changes / auth logic / infrastructure]
- **Original author** cannot approve their own PR
- **Minimum reviewers**: 1 for most PRs; 2 for critical/security changes

---

## Code Review Comment Examples

### Good Comment (Specific, Actionable, Kind)

```
I see this function iterates through the user list for each item, making this O(n²).
Could you optimize using a Set? Something like:

const userSet = new Set(users.map(u => u.id));
Then check `userSet.has(user.id)` instead of the loop.

This would reduce it to O(n).
```

### Bad Comment (Vague, Judgmental)

```
This is inefficient. Rewrite it.
```

---

## Exceptions & Special Cases

- **Hotfixes during outage**: Merge with 1 approval; post-mortem review within 24h
- **Dependency patch updates**: Auto-merge for patch versions (Renovate/Dependabot)
- **Refactoring-only commits**: Lighter review (focus on architectural soundness, not style)
- **Generated code**: Skip style checks (formatters are fine)

---

## Quality Checklist (Before Declaring Standards Ready)

- [ ] Checklist is specific and testable (not vague)
- [ ] Nits and blockers are clearly differentiated
- [ ] Timing expectations are documented
- [ ] Approver tiers are defined
- [ ] Examples of good and bad review comments provided
- [ ] Escalation path is clear
- [ ] Automation is in place (linters, formatters handle style)
- [ ] Team alignment: engineers agree these standards are reasonable

---

## Review Standards Sign-Off

| Property     | Value                 |
| ------------ | --------------------- |
| Owner        | [Tech Lead name]      |
| Created      | [Date]                |
| Last Updated | [Date]                |
| Next Review  | [Date]                |
| Approval     | [Tech Lead signature] |

---

## Process for Updating These Standards

When team needs change standards:

1. Propose changes in a team meeting or GitHub discussion
2. Document rationale (what problem are we solving?)
3. Get consensus from senior engineers
4. Update this document
5. Communicate changes to all engineers (meeting, Slack, docs)
6. Re-baseline expectations (give team 1-2 weeks to adjust)
