---
name: code-review-standards
description: Establish clear, enforceable code review standards that balance quality with velocity, enabling asynchronous review and knowledge sharing. Use when creating or updating review expectations, scaling engineering teams, or improving code quality metrics.
allowed-tools: Read, Grep, Glob, Write, Edit
---

# Code Review Standards

Define explicit code review criteria that scale with your team, enabling reviewers to approve confidently without author present while catching bugs, knowledge gaps, and architectural issues.

## Context

You are helping an engineering leader establish or improve code review standards. Good standards enable async review, spread knowledge, and catch bugs early. Poor standards waste time (nitpicking) or miss issues (insufficient depth).

Code review is an investment: 15 min review per PR catches bugs that might take days to debug in production. But inefficient review (bike-shedding, lack of clear criteria) frustrates teams and slows shipping.

## Domain Context

- **High-performing teams have explicit standards**: Clear criteria remove guesswork; reviewers approve without author present
- **Research (McKinsey)**: Teams with clear code review standards ship 40% faster AND have fewer production defects
- **Code review is about code, not author**: Separate design feedback ("Consider using factory pattern") from style/preference
- **Standards evolve**: As team skill increases, standards can become more ambitious
- **Async review requires clarity**: If criteria are vague, reviewers block waiting for clarification
- **Knowledge sharing**: Code review is a teaching opportunity, not gatekeeping

## When to Use This Skill

- You're establishing standards for a new team
- Code review comments are inconsistent (different standards for different PRs)
- Shipping is slow due to review delays
- Bugs are slipping into production that review should have caught
- You want to scale team size without review becoming a bottleneck

## Prerequisites

Before establishing standards, gather:

1. **Maturity level of the team**: Junior developers (need more hands-on), mid-level (more independence), senior (can own large features)
2. **Code health baseline**: What bugs are slipping through? What's the bug escape rate?
3. **Current review process**: How long does review take? How many rounds?
4. **Team values**: Speed vs. perfection? Risk tolerance?
5. **Business context**: Are you shipping fast (early-stage) or optimizing stability (mature product)?

## Instructions

### 1. Define Review Scope

What requires review?

- **All production code changes**: Yes (including configuration)
- **Documentation**: Yes (README, docs; typos don't need review)
- **Test changes**: Yes (including test infrastructure)
- **Dependency updates**: Yes (new dependencies reviewed; patch updates may be auto-merged)
- **Config/infrastructure**: Yes (even "small" config changes can have big impact)

**Fast-track exceptions** (lighter review):

- Single-line typo fixes
- Documentation corrections
- Reverts of broken code
- Emergency hotfixes during outage (post-mortem review later)

### 2. Create the Review Acceptance Checklist

Define what "approved" means:

**Must have (blocking)**:

- [ ] Code compiles/runs without errors
- [ ] Tests included for new logic; all tests passing
- [ ] No obvious performance regressions (e.g., O(n²) where O(n) exists)
- [ ] Error handling present (don't ignore exceptions; handle edge cases)
- [ ] Security review passed (if code touches auth, payment, data access)
- [ ] Documentation updated (README, comments, API docs if applicable)
- [ ] Follows team style guide (enforced via linter if possible)
- [ ] Minimal complexity increase (no unnecessary abstractions; KISS principle)

**Nice-to-have (not blocking)**:

- [ ] Refactoring opportunities noted (for future work)
- [ ] Performance optimizations suggested (if not critical path)
- [ ] Test coverage >80% (aim for 80%; don't obsess over 100%)

### 3. Clarify Nits vs. Blockers

**Nits** (request only, not requirement):

- Style/formatting (should be auto-enforced by prettier/eslint)
- Naming preferences (code is clear; author's name is reasonable)
- Code comments (code is self-documenting; comment would be nice but not required)
- Unused imports (nice-to-have cleanup)
- Log verbosity (does it log too much/too little? nice-to-have improvement)

**Blockers** (must fix):

- Logic bugs (code doesn't do what it claims)
- Missing tests (no tests for new behavior)
- Security issues (injection, auth bypass, exposed secrets)
- Architectural violations (doesn't fit system design)
- Performance regression (measurable slowdown on critical path)
- Missing error handling (exception could crash service)

### 4. Set Expectations on Time & Process

**Review timing**:

- Target: Code reviewed within 4 business hours
- Approved: Within 8 business hours
- If no response after 8h, author can merge with second reviewer approval

**Review rounds**:

- First pass: Reviewer returns comments
- Author responds: Shows fixes or explains reasoning
- Final approval: No second round needed for trivial fixes; one round typical

**Escalation**:

- If author disagrees with reviewer: Tech lead as tiebreaker
- If reviewer is blocking for subjective reasons: Escalate to tech lead

### 5. Define Who Can Approve

- **Any senior engineer** can approve (more reviewers, faster merges)
- **Specific tech lead** must approve (more careful gate, slower)
- **Original author cannot approve their own PR** (obvious)
- **At least N reviewers** must approve before merge (N=1 for most PRs, N=2 for critical)

### 6. Create Examples & Guidance

Document patterns:

**Good review comment** (specific, actionable, kind):

```
The function iterates through the user list for each item, making this O(n²).
Could you optimize using a Set for lookup? Something like:
const userSet = new Set(users.map(u => u.id));
Then check `userSet.has(user.id)` instead of the loop.
```

**Bad review comment** (vague, judgmental):

```
This is inefficient. Rewrite it.
```

### 7. Establish Escalation Path

- **Disagreement on code design**: Reviewer + author sync in small group; if still stuck, tech lead decides
- **Repeated nit comments from same reviewer**: Tech lead addresses; may indicate over-engineering
- **Blocked PR (no reviewer attention)**: Author pings tech lead; PR unblocked
- **Reviewer blocking unreasonably**: Tech lead discusses standards with reviewer

### 8. Document Exceptions & Special Cases

- **Hotfixes during outage**: Merge with 1 approval; post-mortem review within 24h
- **Dependency updates**: Automated for patch versions; review for minor/major
- **Refactoring-only commits**: Lighter review (focus on architectural soundness, not style)
- **Generated code**: Skip style checks (formatters are fine)

## Output Format

A code review standards document:

```
# Code Review Standards

## Scope
- All production code requires review
- Config, tests, and docs require review
- Fast-track: Single-line typos, documentation-only

## Acceptance Checklist (Blocking)
- [ ] Tests included and passing
- [ ] No obvious performance regressions
- [ ] Error handling present
- [ ] Security reviewed (if applicable)
- [ ] Documentation updated
- [ ] Follows style guide

## Nits vs. Blockers
**Nits**: Style, naming, comments, log verbosity
**Blockers**: Logic bugs, missing tests, security, performance regression

## Timing
- Review target: 4 business hours
- Approval target: 8 business hours
- One round typical; escalate if stuck

## Approvers
- Any senior engineer can approve
- Tech lead for critical/security changes

## Examples
[Code samples showing good/bad comments]

## Escalation
[Process for disagreements, blocked PRs]
```

## Worked Example

**Code Review Standards: Python Backend Team**

### Acceptance Checklist

**Must Have**:

- [ ] Code runs `pytest` without errors
- [ ] Tests included for new functions (minimum: happy path + one error case)
- [ ] All tests passing
- [ ] No `noqa` or `type: ignore` comments unless explicitly approved by tech lead
- [ ] Docstrings present (Google style)
- [ ] No hardcoded secrets (check with `git grep -E '(API_KEY|PASSWORD|TOKEN)'`)
- [ ] Logging at appropriate levels (not verbose on every call)
- [ ] README updated (if user-facing behavior changed)

### Review Guidance

**Example: Good review comment**

```python
# This query could be optimized
users = db.session.query(User).all()
for user in users:
    if user.email == search_email:
        return user

# Suggestion (SQL filter is more efficient):
return db.session.query(User).filter_by(email=search_email).first()
```

**Example: Bad review comment**

```python
This query is inefficient. Fix it.
```

### Nits vs. Blockers

**Nits** (request, not blocking):

- Variable name preference (as long as it's clear)
- Comment suggestions (code is self-explanatory)
- Import order (should be automated)
- Whitespace formatting (should be automated)

**Blockers** (must fix):

- Tests missing for new code
- Exception not handled (could crash in production)
- SQL injection risk (user input in query)
- Type hints missing (team standard)
- Hardcoded password/key

### Timing & Process

- Review within 4 hours of PR submission
- Approval within 8 hours (or author can merge with tech lead approval)
- One review round typical
- If disagreement: Author + reviewer + tech lead (15 min sync)

### Approval

- Any staff engineer+ can approve
- Tech lead approval required for: database schema changes, authentication/authorization logic, infrastructure code

---

## Decision Framework

When reviewing and setting standards:

- **If you're unsure if something is a blocker**: Err on the side of collaborative. Ask: "Can we fix this in a follow-up PR?" if it's non-critical.
- **If you see a pattern of repeated nits from one reviewer**: Have a side conversation. Are they over-engineering?
- **If a PR is blocked and no one is reviewing**: Set a time limit; tech lead unblocks.
- **If standards aren't clear**: Update documentation. Ask the team what's causing confusion.

## Anti-Patterns & Guards

### Anti-Pattern 1: Yak Shaving (Over-Reviewing)

**Description**: Reviewer focuses on variable naming and comment style while missing logic bugs.

**Guard**: Use linters/formatters for style. Reviewers focus on logic, architecture, tests.

### Anti-Pattern 2: Undefined Standards

**Description**: Different reviewers have different expectations; PR gets bounced back multiple times.

**Guard**: Document explicitly. If not in the standards, it's not a blocker.

### Anti-Pattern 3: Junior Devs Reviewing Senior Code

**Description**: Junior developer blocks PR from senior engineer over style preference.

**Guard**: Clear approver tiers. Design decisions reserved for senior/tech lead review.

### Anti-Pattern 4: Standards That Kill Velocity

**Description**: Insisting on tests, refactoring, perfection before merge; ship cycle becomes months.

**Guard**: Prioritize shipping. Non-blocking issues can be follow-ups. Perfection is the enemy of good.

### Anti-Pattern 5: No Follow-Through on "Fix in Next PR"

**Description**: Code reviewed with "Fix this in a follow-up" but follow-up never happens.

**Guard**: Create tracking issue immediately. Link from code review. Revisit quarterly.

## Quality Checklist

Before rolling out standards:

- [ ] **Checklist is specific**: Not vague ("good code"); testable ("tests included")
- [ ] **Nits and blockers are clear**: Reviewers know what's negotiable
- [ ] **Timing expectations set**: Team knows when to expect review
- [ ] **Approver tiers defined**: Clear who can merge
- [ ] **Examples documented**: Show good and bad review comments
- [ ] **Escalation path clear**: What to do if stuck?
- [ ] **Automation in place**: Linters/formatters handle style (not manual review)
- [ ] **Team aligned**: Engineers agree these standards are reasonable

## Further Reading

- McBreen, Pete. _Code Review in High-Performing Teams_ (Agilefant). On code review best practices.
- Forsgren, Nicole et al. _Accelerate: Building and Scaling High Performing Technology Organizations_. IT Revolution Press, 2018. Research on code review and team performance.
- Radigan, Dan. "Code Reviews" (Atlassian Blog). Practical guidance on review.
- Google Engineering Practices: "Code Review Developer Guide" (Public documentation on Google's practices).
