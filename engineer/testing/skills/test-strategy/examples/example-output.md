# Test Strategy: User Authentication Feature

## Feature

User authentication module: login, logout, session management, password reset. Core to system security.

## Test Pyramid

```
E2E (2 tests, 10%):         Complete login/logout flows
Integration (6 tests, 20%):  DB persistence, password hashing, session storage
Unit (28 tests, 70%):        Validation, business logic, edge cases
```

## High-Risk Areas

- **Password handling** (95% coverage): Wrong algo, plaintext storage, timing attack
- **Session management** (95% coverage): Session hijacking, fixation
- **Auth logic** (95% coverage): Wrong user logged in, permission bypass
- **Error messages** (80% coverage): Information disclosure
- **Database queries** (85% coverage): SQL injection, data corruption

## Unit Test Plan (28 tests)

**Password Validation & Hashing**:

- `test_validate_password_rejects_short_password()`
- `test_validate_password_requires_uppercase()`
- `test_validate_password_requires_digit()`
- `test_validate_password_requires_special_char()`
- `test_hash_password_never_returns_plaintext()`
- `test_hash_same_password_produces_different_hashes()` (salt testing)

**Email Validation**:

- `test_validate_email_rejects_missing_at()`
- `test_validate_email_rejects_invalid_domain()`
- `test_validate_email_accepts_valid_format()`

**Login Logic**:

- `test_login_returns_session_token_for_valid_credentials()`
- `test_login_rejects_wrong_password()`
- `test_login_rejects_nonexistent_user()`
- `test_login_rejects_disabled_account()`
- `test_login_increments_failed_attempt_counter()`
- `test_login_locks_account_after_5_failed_attempts()`

**Session Management**:

- `test_generate_session_token_is_cryptographically_random()`
- `test_session_token_expires_after_1_hour()`
- `test_session_validation_rejects_expired_token()`
- `test_session_validation_rejects_tampered_token()`

**Password Reset**:

- `test_reset_token_is_unique_per_request()`
- `test_reset_token_expires_after_24_hours()`
- `test_reset_new_password_must_be_valid()`
- `test_reset_invalidates_all_sessions()`

**Logout**:

- `test_logout_invalidates_session()`
- `test_logout_clears_cookies()`

## Integration Test Plan (6 tests)

- `test_user_registration_saves_hashed_password()` — Password stored securely
- `test_login_retrieves_user_from_database()` — Real DB interaction
- `test_session_token_stored_in_session_table()` — Session persistence
- `test_concurrent_logins_create_separate_sessions()` — No session collision
- `test_failed_login_attempts_logged()` — Audit trail
- `test_password_reset_email_sent_to_verified_address()` — Email service integration

## E2E Test Plan (2 tests)

- `test_full_login_flow()` — Load page → enter credentials → redirect to dashboard
- `test_full_password_reset_flow()` — Click "Forgot password" → enter email → click reset link → new password → login

## Coverage Targets

| Area                | Target | Reason                            |
| ------------------- | ------ | --------------------------------- |
| Password validation | 95%    | High-risk: security critical      |
| Hash generation     | 95%    | High-risk: security critical      |
| Session management  | 95%    | High-risk: prevents hijacking     |
| Login logic         | 95%    | High-risk: core feature           |
| Email validation    | 85%    | Medium-risk: user experience      |
| Error messages      | 80%    | Medium-risk: info disclosure risk |
| Utilities (logging) | 60%    | Low-risk: non-critical            |

**Overall target**: 85% code coverage (higher than typical due to security)

## Test Data Strategy

**Fixtures**:

```
test_user:
  email: "test@example.com"
  password_hash: bcrypt("ValidPassword123!")
  failed_login_attempts: 0
```

**Factories**:

```python
def create_user(email="test@example.com", password="ValidPassword123!"):
    return User(
        email=email,
        password_hash=bcrypt(password),
        created_at=now(),
        verified=True
    )
```

**Mocks**:

```python
mock_email_service.send_reset_email()  # Don't send real emails
mock_random.generate_token()           # Deterministic tokens for testing
```

## Sample Test Code (Unit)

```python
def test_login_rejects_wrong_password():
    # Arrange
    user = create_user(password="ValidPassword123!")

    # Act
    result = auth.login("test@example.com", "WrongPassword!")

    # Assert
    assert result.success is False
    assert result.error == "INVALID_CREDENTIALS"
    assert user.failed_login_attempts == 1  # Counter incremented

def test_session_token_expires_after_1_hour():
    # Arrange
    token = session.generate_token()
    session.store_token(token, expires_at=now() + 1.hour)

    # Act
    time.sleep(1.hour + 1.minute)
    result = session.validate_token(token)

    # Assert
    assert result.valid is False
    assert result.error == "TOKEN_EXPIRED"

def test_password_must_contain_special_character():
    # Arrange
    weak_password = "ValidPassword123"  # No special char

    # Act & Assert
    with pytest.raises(ValueError, match="Must contain special character"):
        auth.validate_password(weak_password)
```

## Success Criteria

- All 36 tests passing (28 unit + 6 integration + 2 E2E)
- 85% overall code coverage
- Password/session/auth areas at 95% coverage
- No flaky tests (all deterministic)
- Test suite runs <5 seconds
- No real emails sent during test runs (mocked)
- Password hashes never logged or exposed

## Real-World Application

Apply similar testing to nullclaw:

- Auth/pairing logic: 95%+ coverage (security critical)
- Tool execution: 90%+ coverage (behavior critical)
- Knowledge graph queries: 80%+ coverage (correctness critical)
- UI formatting: 50%+ coverage (not critical)
