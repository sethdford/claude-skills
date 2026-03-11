# Example: Code Review Standards - Python Backend Team

## Team Context

**Team**: Python Backend (12 engineers, 6 mid-level, 4 senior, 2 junior)

**Tech Stack**: FastAPI, PostgreSQL, Redis, SQLAlchemy ORM

**Service**: Payment processing microservice (revenue-critical)

---

## Scope

**What requires code review**:

- ✅ All production code changes (including config)
- ✅ Database migrations
- ✅ Test files and test infrastructure
- ✅ Dependency changes
- ✅ README, documentation updates

**Fast-track exceptions** (lighter review):

- Single-line typo fixes in docs
- Reverting broken code (if failing tests clearly identified)
- Emergency hotfixes during production outage (reviewed within 24h post-incident)

---

## Acceptance Checklist (Blocking Items)

Code must pass ALL of these before approval:

- [ ] **Tests pass**: `pytest` runs without errors; all tests passing; coverage report generated
- [ ] **Tests included for new logic**: Minimum coverage for new behavior (happy path + 1 error case)
- [ ] **No obvious performance regressions**: No N+1 queries; no synchronous I/O in async context; database queries indexed
- [ ] **Error handling present**: Exceptions caught and logged appropriately; no silent failures
- [ ] **Security review passed** (for auth/payment/PII code): Database queries parameterized (ORM enforces this), no hardcoded secrets, password comparison timing-safe
- [ ] **Documentation updated**: Docstrings follow Google style; README updated if user-facing behavior changed; migration notes if schema changed
- [ ] **Follows style guide**: Enforced by `black` formatter (auto) and `flake8` linter (CI)
- [ ] **Type hints present** (team standard): All function signatures have type hints; no `Any` without explicit justification

---

## Nits vs. Blockers

### Nits (Request Only, Not Blocking)

- Variable naming preferences (code is clear; author's choice is reasonable)
- Docstring improvements (code is self-explanatory; extra docs would be nice)
- Comment suggestions (code is readable; a comment would add context)
- Import ordering (should be auto-enforced by `isort`)
- Test naming conventions (test is clear; different style is fine)

**Example nit comment**:

```
Nice to have: Consider naming this `get_user_by_email_cached`
to make the caching behavior explicit. Current name is fine too.
```

---

### Blockers (Must Fix Before Merge)

- **Logic bugs**: Function doesn't do what PR claims it does
- **Missing tests**: New behavior without test coverage
- **Security vulnerabilities**: Hardcoded secrets, SQL injection risk, timing attacks, privilege escalation
- **Type hint missing**: Function lacks type hints (team standard)
- **Performance regression**: Measurable slowdown on critical path (payment processing, user queries)
- **Exception not handled**: Uncaught exception could crash service in production
- **Database query performance**: N+1 queries, missing index, unparameterized query
- **Breaking API change**: Changes endpoint contract without deprecation

**Example blocker comment**:

```
Blocker: This endpoint changed request format (old clients will break).
Please either:
1. Add backward compatibility layer, or
2. Bump API version and deprecate old endpoint first

Otherwise existing customers get 400 errors.
```

---

## Timing & Process

- **Review target**: 4 business hours from PR submission
- **Approval target**: 8 business hours (if no response, author can merge with secondary approver)
- **One review round typical**: Exceptions for complex logic (2 rounds expected)
- **Escalation path**:
  - Design disagreement → Tech lead + author + reviewer sync (30 min)
  - Reviewer blocking unreasonably → Tech lead intervenes

---

## Approvers

- **Any mid-level+ engineer** can approve standard PRs (API endpoints, business logic)
- **Tech lead or senior engineer** must approve:
  - Database schema changes (migrations, new tables, index changes)
  - Payment processing logic
  - Security/auth code
  - Infrastructure/deployment code
  - API contract changes (backward compatibility important)
- **Original author** cannot approve their own PR
- **Minimum 1 reviewer** for most PRs; **2 reviewers** for critical code

---

## Code Review Examples

### Example 1: Good Blocker Comment

```
Blocker: This endpoint changed from POST to GET, which breaks
all existing clients. Before shipping, either:

Option A: Add a new GET endpoint, keep POST for 3 months with
deprecation warning. Then remove POST.

Option B: Revert to POST and find a different solution.

The current approach will generate support tickets from
customers whose integrations break unexpectedly.
```

**Why it works**:

- Specific (identifies the problem: breaking change)
- Actionable (offers two solutions)
- Explains the impact (customer support burden)
- Kind tone (doesn't blame author)

---

### Example 2: Good Nit Comment

```
Nit: This function handles both cache hit and cache miss.
Consider splitting into `get_user_from_cache()` and
`get_user_from_database()` for clarity. Current approach works fine too.
```

**Why it works**:

- Marked as nit (not required)
- Explains the suggestion (clarity)
- Acknowledges current code is fine

---

### Example 3: Bad Blocker Comment

```
This is inefficient. Rewrite it.
```

**Why it fails**:

- Vague (what's inefficient?)
- Doesn't explain the problem
- No suggested fix
- Author has to guess what to change

---

### Example 4: Bad Nit Comment

```
You should use `snake_case` for variable names. This violates Python conventions.
```

**Why it fails**:

- It's already being enforced by `black` (shouldn't need manual review)
- Marked as blocker language ("should") when it should be nit
- Code already passes linting

---

## Exceptions & Special Cases

- **Hotfixes during outage**: Merge with 1 approval; full review + test within 24h post-incident
- **Dependency patch updates**: Auto-merged by Renovabot (patch versions only)
- **Refactoring-only commits**: 1 reviewer (focus on logic soundness, not style)
- **Generated code** (database models from SQLAlchemy migration): Skip style checks, but verify logic
- **Documentation-only**: 1 reviewer (can be quick)

---

## Enforcement & Automation

| Tool                     | Purpose                      | Enforced Where                  |
| ------------------------ | ---------------------------- | ------------------------------- |
| `black`                  | Code formatting              | CI (fails if not formatted)     |
| `flake8`                 | Linting                      | CI (fails on violations)        |
| `isort`                  | Import ordering              | CI (fails if imports unsorted)  |
| `pytest`                 | Unit tests                   | CI (fails if tests don't pass)  |
| `mypy`                   | Type checking                | CI (fails on type errors)       |
| GitHub branch protection | Require 1 approval + CI pass | Merge button disabled until met |

**Goal**: Reviewers focus on logic and design, not style (automation handles style).

---

## Quality Checklist (Before Team Adoption)

- [x] Checklist is specific (not vague)
- [x] Nits and blockers are clearly differentiated
- [x] Timing expectations documented (4h review, 8h approval)
- [x] Approver tiers defined (mid-level OK for business logic; tech lead for critical)
- [x] Examples of good and bad comments provided
- [x] Escalation path is clear (30-min sync if stuck)
- [x] Automation in place (linters, formatters handle style)
- [x] Team alignment: 12 engineers agree these standards are reasonable

---

## Team Sign-Off

**Status**: ✅ **ADOPTED** 2026-01-15

| Name             | Role            | Sign-Off                    | Date       |
| ---------------- | --------------- | --------------------------- | ---------- |
| Alice Wong       | Tech Lead       | ✅ Approved                 | 2026-01-15 |
| Bob Chen         | Senior Engineer | ✅ Approved                 | 2026-01-15 |
| Carol Smith      | Senior Engineer | ✅ Approved                 | 2026-01-15 |
| Engineering Team | All 12 members  | ✅ Reviewed in team meeting | 2026-01-14 |

---

## Worked Example: Real PR Review

### PR #3891: Payment Processing Refactor

**Description**: Extract payment validation into separate service to reduce code duplication

**Reviewer**: Bob Chen (Senior Engineer)

**Changes**:

- `src/payments/processor.py` (500 lines modified)
- `src/payments/validator.py` (new file, 150 lines)
- `tests/payments/test_validator.py` (new file, 200 tests)

---

### Review Comments

#### Comment 1: Logic Bug (Blocker)

````
Blocker: The amount validation accepts negative amounts.

Current code:
```python
if amount >= 0.01:  # Should be > not >=
    process_payment()
````

This would process $0.01 correctly but negative amounts
would be rejected... actually, it looks correct on second read.

Wait - I see the issue now. The minimum amount is $0.01,
but code checks `>= 0.01`. An amount of $0.001 (0.1 cent)
would fail the check (correct). But this edge case isn't tested.

Please add a test for amounts below minimum:

```python
def test_amount_below_minimum():
    with pytest.raises(ValueError):
        validate_amount(0.001)
```

```

---

#### Comment 2: Type Hints Missing (Blocker)

```

Blocker: Function `validate_amount` is missing type hints.

Current:

```python
def validate_amount(amount):
    return amount >= 0.01
```

Should be:

```python
def validate_amount(amount: float) -> bool:
    """Check if amount meets minimum."""
    return amount >= 0.01
```

Team standard is all functions need type hints.

```

---

#### Comment 3: Performance Question (Nit)

```

Quick question: Does `extract_validator()` get called
for every payment or is it cached? If called every time,
could we cache the validator instance?

Not a blocker - this change is already an improvement
over the original code. Just thinking about future optimization.

```

---

#### Comment 4: Documentation (Blocker)

```

Blocker: The validator module is new. Please add:

1. Module docstring explaining what validation does
2. Docstring for each public function
3. Update README.md with example usage

Example:

```python
\"\"\"Payment validation service.

Ensures all payments meet business rules before processing:
- Amount must be >= $0.01
- Currency must be supported (USD, EUR, GBP)
- Cardholder name cannot be empty
\"\"\"
```

```

---

#### Comment 5: Good Code (Positive Feedback)

```

Really nice: The test coverage is excellent (200 tests, 98% coverage).
Tests are well-organized and clearly named. The edge cases are thorough.
This is exactly the quality we're aiming for.

```

---

### Review Summary

**Status**: Requested Changes (3 blockers, 1 nit)

**Blockers**:
1. Add edge case test for amounts below minimum
2. Add type hints to all functions
3. Add module docstring and function docstrings

**Nit**:
1. Consider caching validator instance (optional)

**Timeline**: Author fixes by next day; re-review scheduled for 10 AM

---

## Quarterly Review Schedule

- **Q1 (Jan-Mar)**: Standards adopted; team gives feedback
- **Q2 (Apr-Jun)**: Review for effectiveness; adjust as needed
- **Q3 (Jul-Sep)**: Check if standards are being followed; any blockers?
- **Q4 (Oct-Dec)**: Annual review; update for next year

**Feedback mechanisms**:
- Slack poll: "Are these standards helpful?" (quarterly)
- Team retro: Any standards causing friction? (monthly)
- Metrics: Average review time, comment quality (monthly dashboard)
```
