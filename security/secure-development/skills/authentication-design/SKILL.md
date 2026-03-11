---
name: authentication-design
description: Design secure authentication systems with strong password policies, MFA, secure password reset, and session management.
---

# Authentication Design

Design secure authentication mechanisms with strong credential policies and multi-factor authentication.

## Context

You are a senior security architect designing authentication for $ARGUMENTS. Authentication is the foundation of access control; a weak authentication system compromises everything downstream.

## Domain Context

- **Authentication** (prove identity): Passwords, biometrics, certificates, hardware tokens, OAuth
- **Authorization** (grant privileges): Roles, permissions, ACLs; implemented after authentication succeeds
- **Session Management** (maintain authenticated state): Tokens, cookies, JWTs; must be protected against hijacking and fixation
- **Multi-Factor Authentication (MFA)**: Second factor (TOTP, FIDO2, SMS) significantly increases security

## Instructions

1. **Password Policy**:
   - Minimum 12 characters (NIST recommends 12+, not 8+)
   - No complexity requirements (NIST 2017 guidance: avoid enforcing special characters, uppercase; users create weak passwords to meet requirements)
   - No password expiration (unless compliance requires; drives users to weak, predictable changes)
   - Must be checked against compromised-password databases (e.g., Have I Been Pwned API)

2. **Password Storage**:
   - Use modern password hashing: **Argon2id** (preferred), bcrypt, or PBKDF2
   - Never MD5, SHA1, or SHA256 (too fast; can be brute-forced)
   - Use high cost/iteration parameters (Argon2: time=2, memory=19 MiB; bcrypt: cost=12; PBKDF2: 100k+ iterations)
   - Use unique salt per password (standard in bcrypt, Argon2)

3. **Multi-Factor Authentication (MFA)**:
   - Require MFA for all user accounts (ideally)
   - Support multiple MFA methods: TOTP (Google Authenticator, Authy), FIDO2 (hardware tokens), SMS (fallback, less secure)
   - Provide backup codes if primary MFA device is lost
   - Never use email as a second factor (email account compromise = game over)

4. **Secure Password Reset**:
   - Email verification required; no password hints that reveal information
   - Reset links: short-lived (30 min), single-use, cryptographically random
   - Require re-authentication before password reset (security question is weak; require knowledge of current password or MFA)
   - Log all password resets; alert user

5. **Session Management**:
   - Use frameworks' built-in session handling (not custom cookies)
   - **HTTPOnly**: Prevent JavaScript access (reduces XSS impact)
   - **Secure**: HTTPS-only transmission
   - **SameSite**: Strict or Lax to prevent CSRF
   - Short expiry (1-24 hours depending on sensitivity)
   - Invalidate on logout
   - Regenerate session ID after login (prevent session fixation)

6. **Credential Transmission**:
   - Always HTTPS; no HTTP for authentication
   - Use POST for credential submission; never GET (credentials in URL history)
   - CSP header to prevent credential interception via malicious scripts

## Anti-Patterns

- Storing passwords in plaintext or with weak hashing (MD5, SHA1); **always use Argon2, bcrypt, or PBKDF2**
- Password expiration policies that drive weak passwords; **modern guidance: strong password + breach detection, not periodic expiration**
- Trusting client-side password strength indicators; **validate server-side, but don't enforce complexity**
- SMS-only 2FA; **SMS is vulnerable to SIM swap; prefer TOTP or FIDO2**
- Allowing password reset via security questions; **these can be guessed or socially engineered; require email or MFA**
- Session tokens with predictable patterns; **use cryptographically random, high-entropy tokens**

## Further Reading

- NIST SP 800-63B (Authentication and Lifecycle Management): https://pages.nist.gov/800-63-3/sp800-63b.html
- OWASP Authentication Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html
- Argon2 Specification: https://github.com/P-H-C/phc-winner-argon2
- Have I Been Pwned API: https://haveibeenpwned.com/API/v3
