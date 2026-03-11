# Example: Secure Code Review - User Registration Feature

## Review Metadata

**Feature**: User Registration & Email Verification (mobile app)

**PR/Commit**: PR #3847 | User registration with verification

**Reviewer**: Jane Smith (Security Lead) | 2026-03-10

**Components Reviewed**:

- `src/auth/registration.py` (main registration logic)
- `src/auth/email_verification.py` (verification token generation)
- `src/auth/password.py` (password hashing)
- Tests: `tests/auth/test_registration.py`

---

## OWASP Top 10 Review Results

### A01 - Broken Access Control

**Questions Asked**:

- Are authorization checks performed before sensitive operations?
- Can users access data they shouldn't?

**Findings**: ✅ **No issues**

- Registration endpoint correctly rejects duplicate email addresses
- Email verification endpoint correctly validates token before activating account
- All database operations check ownership before returning user data

---

### A02 - Cryptographic Failures

**Questions Asked**:

- Is sensitive data encrypted in transit (HTTPS/TLS)?
- Are secure hashing algorithms used (bcrypt/scrypt, not MD5/SHA1)?
- Are encryption keys managed securely (never hardcoded)?

**Findings**: ⚠️ **HIGH severity finding**

```python
# ISSUE: Password hashing uses weak algorithm
from hashlib import sha256

def hash_password(password):
    return sha256(password.encode()).hexdigest()  # ❌ WRONG
```

**Problem**: SHA256 is fast and designed for checksums, not password storage. Attackers can brute-force user passwords at 1B+ hashes/second with modern GPUs.

**Recommendation**:

```python
# CORRECT: Use bcrypt with proper cost factor
from bcrypt import hashpw, gensalt

def hash_password(password):
    salt = gensalt(rounds=12)  # ~100ms per hash on modern CPU
    return hashpw(password.encode(), salt)
```

**Status**: Blocker | Must fix before merge

---

### A03 - Injection

**Questions Asked**:

- Could user input be injected into SQL queries?
- Are parameterized queries used for all database operations?

**Findings**: ⚠️ **CRITICAL severity finding**

```python
# ISSUE: Email verification query vulnerable to SQL injection
def verify_email(email, token):
    query = f"SELECT * FROM users WHERE email = '{email}' AND token = '{token}'"
    return db.execute(query)  # ❌ VULNERABLE
```

**Problem**:

- Attacker can inject SQL: `email = "x' OR '1'='1"; token = "x`
- Would return all users, not just one
- Could be used to bypass verification, activate arbitrary accounts

**Recommendation**:

```python
# CORRECT: Use parameterized queries (ORM or prepared statements)
user = db.query(User).filter(
    User.email == email,
    User.verification_token == token
).first()
```

**Status**: Blocker | Critical security risk

---

### A04 - Insecure Design

**Questions Asked**:

- Is rate limiting implemented for sensitive endpoints?
- Are there controls to prevent brute force attacks?

**Findings**: ⚠️ **HIGH severity finding**

**Issue 1: No rate limiting on registration endpoint**

- Attacker can enumerate valid email addresses (register, get "email already in use")
- Attacker can brute-force verification tokens (99,999 guesses for 5-digit token)

```python
# Add rate limiting
from flask_limiter import Limiter

@limiter.limit("10/hour")  # 10 registrations per hour per IP
def register():
    ...

@limiter.limit("10/minute")  # 10 verification attempts per minute per user
def verify_email():
    ...
```

**Issue 2: Verification token is 5 digits (100,000 combinations)**

- Should be 32+ character random string (2^128 combinations)

```python
# CORRECT: Use secure token
import secrets

def generate_verification_token():
    return secrets.token_urlsafe(32)  # 256-bit security
```

**Status**: Blocker | Multiple design flaws

---

### A05 - Security Misconfiguration

**Questions Asked**:

- Are security headers configured?
- Are defaults secure (fail-closed)?

**Findings**: ✅ **No issues** (handled by infrastructure)

- Framework already sets secure defaults (error messages don't expose stack traces in prod)
- HTTPS enforced at load balancer level
- Cookies marked with httpOnly and Secure flags

---

### A06 - Vulnerable and Outdated Components

**Questions Asked**:

- Are dependencies up to date?
- Are known vulnerabilities present?

**Findings**: 🔍 **Requires follow-up**

`requirements.txt` shows:

- bcrypt 3.2 (latest: 4.0) — OK to update in next PR
- requests 2.25 (latest: 2.31) — VULNERABLE, has security patches

**Recommendation**:

```
requests>=2.31  # Latest version with security patches
```

**Status**: Medium | Must update before merge

---

### A07 - Authentication & Session Management

**Questions Asked**:

- Are passwords hashed with strong algorithms?
- Are sessions properly invalidated on logout?

**Findings**: ⚠️ **MEDIUM severity finding**

**Issue: Verification token not invalidated after use**

```python
# WRONG: Token can be reused indefinitely
def verify_email(email, token):
    user = db.query(User).filter(
        User.email == email,
        User.verification_token == token
    ).first()
    user.verified = True
    db.commit()  # Token still in database!
```

**Problem**: If token is leaked, attacker can re-activate account unlimited times

**Recommendation**:

```python
# CORRECT: Invalidate token after first use
def verify_email(email, token):
    user = db.query(User).filter(...).first()
    if not user or user.verification_token != token:
        return error("Invalid token")
    if user.verified:
        return error("Already verified")

    user.verified = True
    user.verification_token = None  # Invalidate
    user.verification_token_expires_at = None
    db.commit()
```

**Also**: Add expiration to tokens:

```python
# Tokens should expire after 24 hours
from datetime import datetime, timedelta

if datetime.utcnow() > user.verification_token_expires_at:
    return error("Token expired")
```

**Status**: Blocker | Token reuse vulnerability

---

### A08 - Software & Data Integrity Failures

**Findings**: ✅ **No issues**

- Dependencies pinned to known-good versions
- No remote code execution vectors
- No dynamic code loading

---

### A09 - Logging & Monitoring

**Questions Asked**:

- Are security-relevant events logged?
- Are secrets/PII excluded from logs?

**Findings**: ⚠️ **MEDIUM severity finding**

```python
# WRONG: Logs contain sensitive information
logger.info(f"User registered: {email}, password={password}")  # ❌ Don't log password!
```

**Recommendation**:

```python
# CORRECT: Log only metadata, no secrets
logger.info(f"User registration attempt", extra={
    "email_hash": hashlib.sha256(email.encode()).hexdigest()[:8],
    "source_ip": request.remote_addr,
    "timestamp": datetime.utcnow().isoformat()
})

# Log successful registration (no email/password)
logger.info("User registration successful", extra={"user_id": user.id})

# Log security events
logger.warning("Email verification failed", extra={"attempts": 5, "user_id": user.id})
```

**Status**: Blocker | PII in logs is a GDPR violation

---

### A10 - SSRF

**Findings**: ✅ **No issues**

- No external URL requests in registration flow
- Email sending handled by separate service (not exposed here)

---

## Summary of Findings

| Severity | Count | Details                                                            |
| -------- | ----- | ------------------------------------------------------------------ |
| Critical | 1     | SQL injection in email verification                                |
| High     | 2     | Weak password hashing, no rate limiting, insecure token generation |
| Medium   | 2     | Token reuse, PII in logs                                           |
| Low      | 1     | Dependency update needed                                           |

---

## Detailed Recommendations

### Blockers (Must Fix Before Merge)

1. **Replace SHA256 with bcrypt** for password hashing
2. **Fix SQL injection** in email verification query
3. **Implement rate limiting** on registration and verification endpoints
4. **Generate 32+ character tokens** for email verification (not 5 digits)
5. **Invalidate tokens** after first use
6. **Add token expiration** (24 hours)
7. **Remove PII from logs** (emails, passwords)
8. **Update `requests` dependency** to latest version

### Follow-Up Issues (Can File as Tickets)

- [ ] Add CAPTCHA to registration to prevent spam
- [ ] Implement email verification email template (with security warnings)
- [ ] Add account lockout after 5 failed verification attempts
- [ ] Implement password reset endpoint (same security standards)

---

## Code Review Comments (For GitHub)

### Comment 1: Password Hashing

```
Blocker: This uses SHA256 for password hashing, which is too fast for password storage.
With modern GPUs, attackers can brute-force at 1B+ hashes/second.

Please use bcrypt with at least 12 rounds:

from bcrypt import hashpw, gensalt

def hash_password(password):
    salt = gensalt(rounds=12)
    return hashpw(password.encode(), salt)

This will add ~100ms latency per password hash (acceptable for registration).
```

### Comment 2: SQL Injection

````
Blocker: This email verification query is vulnerable to SQL injection.

Current code:
```python
query = f"SELECT * FROM users WHERE email = '{email}' AND token = '{token}'"
````

Attacker can pass: email = "x' OR '1'='1" and return all users.

Use an ORM or parameterized query:

```python
user = db.query(User).filter(
    User.email == email,
    User.verification_token == token
).first()
```

```

### Comment 3: Rate Limiting
```

Blocker: No rate limiting on registration/verification endpoints.

Attacker can:

1. Enumerate valid emails (register, see "email in use")
2. Brute-force verification tokens (5 digits = 100K attempts)

Add rate limiting:

```python
@limiter.limit("10/hour")
def register():
    ...

@limiter.limit("10/minute")
def verify_email():
    ...
```

```

### Comment 4: Token Security
```

High severity: Verification tokens are only 5 digits. Should be 32+ characters.

Change from:

```python
token = random.randint(10000, 99999)  # 100K combinations
```

To:

```python
token = secrets.token_urlsafe(32)  # 2^256 combinations
```

```

### Comment 5: Token Reuse
```

Blocker: Tokens are not invalidated after first use. An attacker who leaks the token
can re-activate the account indefinitely.

After verification, set:

```python
user.verification_token = None
user.verification_token_expires_at = None
```

```

### Comment 6: PII in Logs
```

Blocker: This logs email addresses and passwords, violating GDPR data minimization.

Don't log PII. Instead:

```python
logger.info("User registration", extra={
    "email_hash": hashlib.sha256(email.encode()).hexdigest()[:8],
    "source_ip": request.remote_addr
})
```

````

---

## Recommended Actions

**Before Merge**:
- [ ] All Critical/High findings addressed (8 blockers above)
- [ ] Tests added for each security fix
- [ ] Code re-reviewed after fixes

**Follow-Up Issues**:
- [ ] CAPTCHA to prevent registration spam
- [ ] Account lockout mechanism (5 failed verifications)
- [ ] Email template security warnings

---

## Test Coverage

**New tests needed**:
```python
def test_password_hashing_uses_bcrypt():
    # Verify password hash is not a simple hash
    hash1 = hash_password("password123")
    hash2 = hash_password("password123")
    assert hash1 != hash2  # Bcrypt uses salt, so hashes differ

def test_sql_injection_protection():
    # Attempt SQL injection
    result = verify_email("x' OR '1'='1", "fake_token")
    assert result is None  # Should fail, not return user

def test_rate_limiting_registration():
    # 11 registrations should trigger rate limit
    for i in range(11):
        result = register(f"user{i}@example.com")
    # 11th should fail with 429 Too Many Requests
    assert result.status_code == 429

def test_token_expiration():
    # Token should expire after 24 hours
    token = generate_verification_token()
    user.verification_token_expires_at = datetime.utcnow() - timedelta(days=1)
    result = verify_email(user.email, token)
    assert result is None  # Token expired
````

---

## Sign-Off

**Status**: 🔴 **BLOCKED - Resubmit**

**Reasoning**: 1 critical + 2 high severity findings must be fixed before merge. These are fundamental security flaws (SQL injection, weak password hashing) that would leave users vulnerable.

**Reviewer**: Jane Smith (Security Lead)
**Date**: 2026-03-10

**Next Steps**:

1. Fix all 8 blockers (estimated 2-3 hours of work)
2. Add tests for each fix
3. Request re-review once fixed
