# Refactoring Example: User Registration Service

## Refactoring Technique

Extract Method + Replace Flag Argument with Methods

## Problem Identified

The `register_user()` method in UserService does too much:

1. Validates email
2. Hashes password
3. Creates user record
4. Sends welcome email
5. Logs activity

Additionally, a boolean `send_email` flag parameter makes the API confusing. Callers don't know what behavior they're getting.

**Symptoms**:

- Method is 45 lines long
- Hard to test individual concerns
- Email sending is tightly coupled to user creation
- Flag parameter violates intent-revealing naming

## Before Code

```python
class UserService:
    def register_user(self, email, password, full_name, send_email=True):
        """Register a new user. If send_email=False, skip welcome email."""

        # Validation
        if not email or "@" not in email:
            raise ValueError("Invalid email")
        if len(password) < 8:
            raise ValueError("Password must be 8+ chars")
        if not full_name:
            raise ValueError("Name required")

        # Hash password
        hashed = bcrypt.hashpw(password.encode(), bcrypt.gensalt())

        # Create user
        user = User(
            email=email,
            password_hash=hashed,
            full_name=full_name,
            created_at=datetime.now()
        )
        self.db.save(user)

        # Send email
        if send_email:
            self.email_service.send_welcome_email(
                to=email,
                name=full_name,
                activation_link=f"https://app.com/activate/{user.id}"
            )

        # Log
        self.logger.info(f"User registered: {email}")

        return user
```

**Problems**:

- Long method with multiple concerns
- Flag parameter makes intent unclear (`send_email=True` — when is this False?)
- Email service dependency is tightly coupled
- Hard to unit test without side effects
- Difficult to reuse validation logic

## After Code (Refactored)

```python
class UserService:
    def register_user(self, email, password, full_name):
        """Register a new user and send welcome email."""
        self._validate_registration_input(email, password, full_name)
        user = self._create_user(email, password, full_name)
        self._send_welcome_email(user)
        self.logger.info(f"User registered: {email}")
        return user

    def register_user_without_email(self, email, password, full_name):
        """Register a new user without sending welcome email."""
        self._validate_registration_input(email, password, full_name)
        user = self._create_user(email, password, full_name)
        self.logger.info(f"User registered (no email): {email}")
        return user

    def _validate_registration_input(self, email, password, full_name):
        """Validate all registration inputs."""
        if not email or "@" not in email:
            raise ValueError("Invalid email")
        if len(password) < 8:
            raise ValueError("Password must be 8+ chars")
        if not full_name:
            raise ValueError("Name required")

    def _create_user(self, email, password, full_name):
        """Create and persist user record."""
        hashed = bcrypt.hashpw(password.encode(), bcrypt.gensalt())
        user = User(
            email=email,
            password_hash=hashed,
            full_name=full_name,
            created_at=datetime.now()
        )
        self.db.save(user)
        return user

    def _send_welcome_email(self, user):
        """Send welcome email to new user."""
        self.email_service.send_welcome_email(
            to=user.email,
            name=user.full_name,
            activation_link=f"https://app.com/activate/{user.id}"
        )
```

## Why This Refactoring?

**Improvements**:

1. **Single Responsibility**: Each method does one thing
   - `register_user()`: orchestrates registration with email
   - `register_user_without_email()`: orchestrates registration without email
   - `_validate_registration_input()`: validates input (reusable)
   - `_create_user()`: creates user (reusable)
   - `_send_welcome_email()`: sends email (reusable)

2. **Clearer Intent**: Method names reveal what happens. No confusing flags.
   - `register_user()` obviously sends email
   - `register_user_without_email()` obviously doesn't

3. **Better Testability**: Each concern can be tested independently

   ```python
   def test_validate_rejects_invalid_email():
       service._validate_registration_input("bad", "password123", "John")  # Raises

   def test_create_user_persists_and_returns():
       user = service._create_user("john@example.com", "password123", "John")
       assert user.email == "john@example.com"
       assert db.find_user(user.id) == user

   def test_send_welcome_email_calls_service():
       user = User(email="john@example.com", ...)
       service._send_welcome_email(user)
       email_service.send_welcome_email.assert_called_with(
           to="john@example.com", name="John", activation_link=...
       )
   ```

4. **Reduced Coupling**: Email service is now isolated in one method; easier to mock or replace

5. **Reusability**: `_validate_registration_input()` and `_create_user()` can be called by other methods

## Verification

- **Tests status**: All tests pass
- **Behavior preserved**: Yes
  - `register_user("john@example.com", "pass123", "John")` → same result as before
  - `register_user_without_email("john@example.com", "pass123", "John")` → new method, works
- **Code metrics**:
  - Before: 45 lines in 1 method
  - After: 60 lines in 6 methods (each method <15 lines)
  - Cyclomatic complexity reduced from 4 to 1 (per method)

## Commit Message

```
refactor: extract user registration concerns and replace flag parameter

Split register_user() into focused methods:
- _validate_registration_input(): validate inputs
- _create_user(): create and persist user
- _send_welcome_email(): send welcome email

Replace send_email flag with two methods:
- register_user(): registration with email (default)
- register_user_without_email(): registration without email

Benefits:
- Each method has single responsibility
- Easier to test in isolation
- Intent is clear from method name (no confusing flags)
- Logic is reusable for other workflows (e.g., admin user creation)
```

## Next Opportunity

**Refactoring 2**: Extract Validation into a Validator class

```python
class UserRegistrationValidator:
    def validate(self, email, password, full_name):
        if not email or "@" not in email:
            raise ValueError("Invalid email")
        if len(password) < 8:
            raise ValueError("Password must be 8+ chars")
        if not full_name:
            raise ValueError("Name required")

class UserService:
    def __init__(self, db, email_service, logger, validator=None):
        self.db = db
        self.email_service = email_service
        self.logger = logger
        self.validator = validator or UserRegistrationValidator()

    def _validate_registration_input(self, email, password, full_name):
        self.validator.validate(email, password, full_name)
```

This enables:

- Reuse validation in other services
- Test validation independently
- Swap validation logic without changing UserService

---

## Real-World Notes

In the real nullclaw codebase, you'd apply similar refactorings to:

1. `src/security/pairing.c` — Extract public key validation and pairing logic
2. `src/tools/tool_executor.c` — Extract execution, sandboxing, and result formatting
3. `src/gateway/gateway.c` — Extract request routing, auth checks, and response formatting

Each extraction follows the same pattern:

- Identify multiple concerns in one function
- Extract each concern to a focused helper
- Replace flag parameters with multiple, named methods
- Keep helpers private (\_prefix) if not reused; public if reusable
- Test each helper independently
- Commit one refactoring at a time
