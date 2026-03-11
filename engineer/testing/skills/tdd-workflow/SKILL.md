---
name: tdd-workflow
description: Red-Green-Refactor cycle for test-first development. Write failing test, implement minimal code, refactor safely. Use when developing new features or fixing bugs in test-driven projects.
context: fork
agent: general-purpose
allowed-tools: Read, Grep, Glob, Write, Edit, Bash
---

# TDD Workflow

Disciplined test-first development with the Red-Green-Refactor cycle. Tests shape API design; fearless refactoring becomes possible.

## Context

You are guiding the engineer through TDD. Your role is to help them:

- Write clear, focused tests that describe desired behavior before implementation
- Implement minimal code that passes the test (no over-engineering)
- Refactor with confidence, knowing tests will catch mistakes
- Keep cycles short (5-15 minutes) to maintain momentum
- Use test failures as design feedback

TDD is not just about testing; it's about using tests as a design tool to improve code clarity and maintainability.

## Domain Context

Based on Kent Beck, Bob Martin, and J.B. Rainsberger:

- **Red Phase**: Write test describing desired behavior; it fails because feature doesn't exist. This failure is essential—it proves the test actually tests something.
- **Green Phase**: Write minimal code to pass the test. "Minimal" means: just enough logic; no premature optimization; no extra features.
- **Refactor Phase**: Improve code without changing behavior. Extract methods, improve names, reduce duplication. Tests protect against regressions.
- **Design Feedback**: If tests are hard to write, the API is hard to use. If mocking is complex, coupling is too tight. Tests reveal design problems early.
- **Regression Safety**: Previous tests continue passing, so refactoring is fearless. This enables continuous improvement.
- **Cycle Length**: 5-15 minutes per cycle. Longer cycles indicate the test is too complex; break it down.

## When to Use This Skill

- Starting a new feature where behavior is well-defined
- Fixing a bug (write test for the bug first, then implement fix)
- Adding to a codebase already using TDD (maintain consistency)
- When you want to confidently refactor without fear of regressions
- When API design is uncertain (tests force clarity)

## Prerequisites

Before starting TDD, confirm:

- **Clear Requirements**: Understand what "done" looks like for this feature
- **Test Framework**: Know how to write tests in your language (unittest, pytest, Jest, xUnit)
- **Development Environment**: Can run tests locally in <5 seconds
- **Existing Tests**: Review existing tests to match style and patterns
- **Integration Plan**: Where will this code plug into the system?

## Instructions (Detailed)

### 1. **Understand the Feature**

Read requirements carefully. Ask clarifying questions:

- What is the input? What is the expected output?
- What are edge cases or error conditions?
- How does this interact with existing code?
- What business value does this provide?

Write down the acceptance criteria. These become test cases.

### 2. **Write the First Failing Test (Red)**

Write a single test that describes one piece of desired behavior. Make it fail.

Example (Python):

```python
def test_user_email_validation_rejects_missing_at_symbol():
    # Arrange
    validator = EmailValidator()
    # Act
    is_valid = validator.is_valid("userexample.com")
    # Assert
    assert is_valid is False
```

Rules for this phase:

- **One assertion per test** (or tightly related assertions)
- **Clear name**: `test_<subject>_<condition>_<expected_outcome>`
- **Test behavior, not implementation**: Don't test private methods; test observable behavior
- **Arrange-Act-Assert**: Set up state, call code, verify outcome
- **Make it fail first**: Run the test; confirm it fails with the error you expect

### 3. **Implement Minimal Code (Green)**

Write the simplest code that passes the test. No optimization, no extra features.

Example (Python):

```python
class EmailValidator:
    def is_valid(self, email: str) -> bool:
        return "@" in email
```

This is deliberately naive. It passes the test. Now the test can guide the next iteration.

Rules for this phase:

- **No premature optimization**: Avoid performance tweaks; optimize when profiling shows a problem
- **No extra features**: Implement only what the test requires
- **Copy-paste is acceptable**: Duplication is fixed in Refactor phase
- **Comment if unclear**: If you needed to think hard, add a comment for future readers

### 4. **Verify the Test Passes (Green)**

Run the test. It should pass.

```bash
python -m pytest test_email_validator.py::test_user_email_validation_rejects_missing_at_symbol -v
```

If it fails, debug the implementation, not the test. The test defines correctness.

### 5. **Check Existing Tests Still Pass**

Run the full test suite. No regressions.

```bash
python -m pytest tests/
```

If an existing test breaks, you've changed behavior unintentionally. Fix the implementation.

### 6. **Refactor (Refactor)**

Now improve the code: better names, extract methods, reduce duplication. Tests protect you.

Example: The naive implementation passes one test. Write the next test for a positive case:

```python
def test_user_email_validation_accepts_valid_email():
    validator = EmailValidator()
    assert validator.is_valid("user@example.com") is True
```

This test fails (your naive implementation doesn't validate the domain). Now refactor:

```python
class EmailValidator:
    def is_valid(self, email: str) -> bool:
        if not email or "@" not in email:
            return False
        local, domain = email.rsplit("@", 1)
        if not local or not domain or "." not in domain:
            return False
        return True
```

Run all tests. Both pass. The implementation evolved because tests revealed missing behavior.

### 7. **Repeat: Write Next Test**

Start again at step 2. Each cycle improves the implementation and test coverage.

Example test sequence for email validator:

1. Test missing @ → minimal implementation
2. Test valid email → refactor to handle domain
3. Test spaces in email → refactor validation
4. Test multiple @ symbols → refactor parsing
5. Test empty local part → refactor
6. Eventually: regex or use a library

Each test adds one behavioral requirement. The implementation grows steadily, staying simple.

### 8. **Watch for Long Cycles**

If a cycle takes >15 minutes:

- Break test into smaller pieces (test one behavior per test)
- Implementation might need a helper function (implement with next test)
- You might be over-engineering; step back and check requirements

## Output Format

When using this skill, deliver:

1. **Test Code**: Failing test demonstrating desired behavior (Red)
2. **Implementation**: Minimal code passing the test (Green)
3. **Refactored Code**: Improved implementation if duplication emerged (Refactor)
4. **Test Suite Status**: All tests passing, no regressions
5. **Next Test**: What behavior should the next test verify?

Example output structure:

```
## Red: Write Test
[test code showing failure]

## Green: Implement
[minimal implementation]

## Verify
- Test passes: ✓
- Suite passes: ✓
- No regressions: ✓

## Refactor (if needed)
[improved code with better names/structure]

## Next Cycle
The next test should verify [specific behavior], because [reason].
```

## Worked Example

**Feature**: User password strength validator

**Requirement**: Passwords must be 8+ characters, contain uppercase, lowercase, digit, and special character.

### Cycle 1: Test minimum length

**Red: Test**

```python
def test_password_rejects_too_short():
    validator = PasswordValidator()
    assert validator.is_strong("Pass1!") is False  # 6 chars, needs 8
```

**Green: Implement**

```python
class PasswordValidator:
    def is_strong(self, password: str) -> bool:
        return len(password) >= 8
```

**Verify**: Test passes. Suite passes.

### Cycle 2: Test requires uppercase

**Red: Test**

```python
def test_password_rejects_missing_uppercase():
    validator = PasswordValidator()
    assert validator.is_strong("password1!") is False  # no uppercase
```

**Green: Implement**

```python
class PasswordValidator:
    def is_strong(self, password: str) -> bool:
        if len(password) < 8:
            return False
        return any(c.isupper() for c in password)
```

**Verify**: Both tests pass.

### Cycle 3: Test requires lowercase

**Red: Test**

```python
def test_password_rejects_missing_lowercase():
    validator = PasswordValidator()
    assert validator.is_strong("PASSWORD1!") is False  # no lowercase
```

**Green: Implement**

```python
class PasswordValidator:
    def is_strong(self, password: str) -> bool:
        if len(password) < 8:
            return False
        if not any(c.isupper() for c in password):
            return False
        return any(c.islower() for c in password)
```

**Verify**: All three tests pass.

### Cycle 4: Test requires digit

**Red: Test**

```python
def test_password_rejects_missing_digit():
    validator = PasswordValidator()
    assert validator.is_strong("Password!") is False  # no digit
```

**Green: Implement**

```python
class PasswordValidator:
    def is_strong(self, password: str) -> bool:
        if len(password) < 8:
            return False
        if not any(c.isupper() for c in password):
            return False
        if not any(c.islower() for c in password):
            return False
        return any(c.isdigit() for c in password)
```

**Verify**: All four tests pass.

### Cycle 5: Test requires special character

**Red: Test**

```python
def test_password_rejects_missing_special_char():
    validator = PasswordValidator()
    assert validator.is_strong("Password1") is False  # no special char
```

**Green: Implement**

```python
class PasswordValidator:
    SPECIAL_CHARS = "!@#$%^&*()-_=+[]{}|;:',.<>?/`~"

    def is_strong(self, password: str) -> bool:
        if len(password) < 8:
            return False
        if not any(c.isupper() for c in password):
            return False
        if not any(c.islower() for c in password):
            return False
        if not any(c.isdigit() for c in password):
            return False
        return any(c in self.SPECIAL_CHARS for c in password)
```

**Verify**: All five tests pass.

### Cycle 6: Refactor

Notice repetition in validation checks. Extract helper:

```python
class PasswordValidator:
    SPECIAL_CHARS = "!@#$%^&*()-_=+[]{}|;:',.<>?/`~"

    def is_strong(self, password: str) -> bool:
        return (
            self._has_min_length(password, 8)
            and self._has_uppercase(password)
            and self._has_lowercase(password)
            and self._has_digit(password)
            and self._has_special_char(password)
        )

    def _has_min_length(self, password: str, length: int) -> bool:
        return len(password) >= length

    def _has_uppercase(self, password: str) -> bool:
        return any(c.isupper() for c in password)

    def _has_lowercase(self, password: str) -> bool:
        return any(c.islower() for c in password)

    def _has_digit(self, password: str) -> bool:
        return any(c.isdigit() for c in password)

    def _has_special_char(self, password: str) -> bool:
        return any(c in self.SPECIAL_CHARS for c in password)
```

**Verify**: All tests still pass. Refactoring complete.

### Cycle 7: Test happy path

**Red: Test**

```python
def test_password_accepts_valid_strong_password():
    validator = PasswordValidator()
    assert validator.is_strong("MyPass1!") is True
```

**Green**: Already implemented; test passes immediately.

## Decision Framework

When writing tests, use these decisions:

- **If unclear how feature should behave**: Write a test capturing your understanding. Discuss with product owner.
- **If implementation is taking >15 min**: Break cycle into smaller test. Implementation is too complex for one test.
- **If test is hard to write**: Consider design. Is the API easy to use? Does it have too many dependencies?
- **If test requires complex mocking**: Implementation has tight coupling. Consider refactoring.
- **If test passes without new implementation**: Test is redundant; skip it or combine with another test.
- **If adding feature breaks existing tests**: Don't change tests; fix implementation to satisfy both old and new requirements.

## Anti-Patterns (Expanded)

### 1. **Skipping Red Phase**

**Mistake**: Write code, then write tests afterward.

**Why LLMs make this**: Implementing feels like progress; tests feel like overhead. Code-first pressure is high.

**Guard**: Before writing any implementation, write a test that currently fails. Run it; confirm failure message is clear.

**Example**:

- Bad: Write `EmailValidator.is_valid()` implementation, then write test
- Good: Write test that fails, then implement `is_valid()`

---

### 2. **Writing Tests After Code**

**Mistake**: Implement feature; then write tests to verify it works.

**Why LLMs make this**: Tests are supposed to document behavior; code already documents behavior.

**Guard**: Tests written first reveal design problems that post-hoc tests miss. Make it a workflow rule.

**Example**:

- Bad: Implement `UserService.create_user()`, then write test
- Good: Write test of `UserService.create_user()` first; implement after

---

### 3. **Over-Engineering in Green Phase**

**Mistake**: Implement "production-quality" code on first pass (optimization, generalization, error handling).

**Why LLMs make this**: Training emphasizes complete, robust implementations.

**Guard**: If implementation doesn't feel deliberately naive, you're over-engineering. Write simplest code that passes test; refactor later.

**Example**:

- Bad: Implement regex email validation on first test; refactor later
- Good: Implement `"@" in email` on first test; evolve with each test

---

### 4. **Not Running Tests Frequently**

**Mistake**: Write multiple tests without running; run them all at once.

**Why LLMs make this**: Batching feels efficient.

**Guard**: Run tests after each Red-Green-Refactor cycle. Rapid feedback (minutes, not hours) reveals problems immediately.

**Example**:

- Bad: Write 5 tests, implement 5 features, run tests once
- Good: Red-Green-Refactor each test individually; run after each cycle

---

### 5. **Refactoring Without Running Tests**

**Mistake**: Refactor code, then run tests later; hope nothing broke.

**Why LLMs make this**: Large refactors feel productive.

**Guard**: Before refactoring, tests must pass. After each small refactoring step (rename, extract, move), run tests. If tests fail, revert and try smaller step.

**Example**:

- Bad: Refactor entire validation class; run tests once at end
- Good: Rename one variable, run tests; extract one method, run tests; repeat

---

### 6. **Unclear Test Names**

**Mistake**: Write tests with names like `test_email()` or `test_password_1()`.

**Why LLMs make this**: Generating descriptive names takes extra effort.

**Guard**: Test name should describe the condition and expected outcome. Read the test name aloud; does it explain what's being tested?

**Example**:

- Bad: `test_email()`, `test_password_validation()`
- Good: `test_email_validation_rejects_missing_at_symbol()`, `test_password_validator_requires_min_8_chars()`

---

## Quality Checklist

Before considering a test complete, verify:

- [ ] **Test name clearly describes behavior tested** — Read aloud; is it understandable?
- [ ] **Test currently fails** (Red phase) — Run it; confirm it fails as expected
- [ ] **Minimal implementation passes test** (Green phase) — Implementation should feel naive, not complete
- [ ] **All existing tests still pass** — No regressions introduced
- [ ] **Test uses Arrange-Act-Assert** — Setup, call code, verify result
- [ ] **One logical assertion per test** — Test one behavior; separate tests for edge cases
- [ ] **No test interdependencies** — Tests can run in any order, independently
- [ ] **Refactored code is cleaner** — After Refactor phase, code should be easier to read
- [ ] **Next test is identified** — What behavior should the next cycle verify?
- [ ] **Cycle time was <15 minutes** — If longer, next test should be smaller

## Further Reading

- **Kent Beck**, _Test-Driven Development: By Example_ (2002) — Foundational; essential reading. Walks through real TDD examples with money and xUnit.
- **Robert C. Martin**, _Clean Code_ (2008), Chapter 9 — Focuses on unit test quality: readability, independence, cleanliness.
- **J.B. Rainsberger**, _Integrated Tests Are a Scam_ (2010) — Why isolated unit tests + TDD beats integration test-first approaches.
- **Roy Osherove**, _The Art of Software Testing_ (2nd ed., 2011) — TDD strategy, test coverage, test maintainability.
- **Steve Freeman & Nat Pryce**, _Growing Object-Oriented Software, Guided by Tests_ (2009) — TDD in practice on real projects; mockist testing approach.
- **Sandro Mancuso**, _The Software Craftsman_ (2014) — Professionalism, TDD, and continuous improvement discipline.
