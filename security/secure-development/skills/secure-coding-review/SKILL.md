---
name: secure-coding-review
description: Review code systematically for security vulnerabilities using OWASP Top 10, secure coding patterns, and static analysis best practices. Use when reviewing pull requests, conducting security code reviews, or implementing secure development practices.
allowed-tools: Read, Grep, Glob, Write, Edit
---

# Secure Coding Review

Conduct systematic code reviews for security vulnerabilities, focusing on input validation, authentication, authorization, cryptography, and error handling.

## Context

You are a security-focused code reviewer helping catch vulnerabilities before they reach production. Code review is the first line of defense against exploitable flaws. Many breaches result from coding mistakes that could have been caught with disciplined review.

Unlike functional code review (which focuses on logic, style, performance), security review asks: "What could an attacker do with this code?"

## Domain Context

- **OWASP Top 10 (2021)**: Industry standard for critical web vulnerabilities (A01-A10)
- **CWE Top 25**: Most dangerous software weaknesses (input validation, buffer overflow, SQL injection, cross-site scripting, broken auth)
- **Secure coding principles**:
  - Input validation (whitelist, not blacklist; validate type, length, format, range)
  - Output encoding (context-specific: HTML, URL, JavaScript, SQL)
  - Authentication (never trust client-side; use established libraries)
  - Authorization (least privilege; check on every action, not just entry)
  - Cryptography (use vetted libraries; never implement custom crypto)
  - Error handling (never expose sensitive info in error messages)
- **Defense in depth**: Multiple layers of security; don't rely on any single control
- **Secure by default**: Safe defaults; require explicit opt-in for risky behavior

## When to Use This Skill

- A team member submitted a PR touching authentication, payment processing, or data access
- You're implementing a new integration with third-party APIs or databases
- You're building a feature that handles user input, file uploads, or privileged actions
- You're reviewing code after a security vulnerability is discovered
- You want to establish secure coding practices in your team

## Prerequisites

Before reviewing, gather:

1. **Code context**: Understand what the code does and who uses it
2. **Attack surface**: Where does untrusted input enter the system?
3. **Data classification**: What sensitive data is touched (PII, credentials, payment info)?
4. **Security requirements**: Are there compliance needs (PCI-DSS, HIPAA, SOC2)?
5. **Existing controls**: What security measures are already in place?

## Instructions

### 1. Identify Privileged Code Paths

Focus review on high-risk areas:

- Authentication and authorization logic
- Input handling and parsing (forms, APIs, file uploads)
- Cryptographic operations
- Database queries (especially with user input)
- Privilege escalation opportunities (admin functions, special permissions)
- External API integrations
- Error handling and logging

### 2. Check for OWASP Top 10 Vulnerabilities

| Vulnerability                          | What to Look For                                                      | Red Flag                                                                                       |
| -------------------------------------- | --------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **A01: Broken Access Control**         | Can user bypass authorization? Are permission checks on every action? | User can edit others' data with ID manipulation; POST endpoints don't check authorization      |
| **A02: Cryptographic Failures**        | Is sensitive data encrypted? At rest and in transit?                  | Passwords stored in plaintext; hardcoded API keys; unencrypted database columns                |
| **A03: Injection (SQL, OS, template)** | Is all input parameterized?                                           | SQL query built with string concatenation; shell commands with user input                      |
| **A04: Insecure Design**               | Are security requirements captured? Was threat modeling done?         | Feature has no authentication requirements; design assumes all users are trusted               |
| **A05: Security Misconfiguration**     | Are defaults secure?                                                  | Debugging enabled in production; unnecessary services running; default credentials not changed |
| **A06: Vulnerable Components**         | Are dependencies up-to-date?                                          | Using EOL library; known CVE in dependency; no dependency scanning                             |
| **A07: Authentication Failures**       | Can password be brute-forced? Is MFA enforced?                        | No rate limiting on login; no account lockout; plaintext password transmission                 |
| **A08: Data Integrity Failures**       | Can data be modified by attacker?                                     | No CSRF token; insecure deserialization; unsigned API responses                                |
| **A09: Logging & Monitoring Failures** | Are suspicious activities logged?                                     | Successful login not logged; failed auth not tracked; no alerting on repeated failures         |
| **A10: SSRF**                          | Can attacker reach internal services?                                 | URL from user input passed to HTTP client without validation; internal IPs accessible          |

### 3. Validate Input Handling

For every input source (form, API, file, database, config), verify:

- **Input is validated**: Length, type, format, range checked before use
- **Validation is positive (whitelist)**: Define what's ALLOWED, not what's blocked
- **Sanitization happens**: Special characters escaped for the context (SQL, HTML, URL, etc.)
- **No string concatenation for SQL**: Use parameterized queries or prepared statements
- **File uploads checked**: File type (magic bytes, not extension), size, scanned for malware
- **Output is context-specific**: HTML output entity-encoded; URLs encoded; JavaScript escaped

### 4. Review Authentication & Authorization

Ask:

- **Authentication**: Is identity verified securely? (Never trust client-side; use HTTPS; no default credentials)
- **Session management**: Are sessions invalidated after logout? Tokens have short TTLs?
- **Password policy**: Are weak passwords rejected? (Min length 12, complexity not enforced, but length is)
- **MFA**: Is MFA available for sensitive actions?
- **Authorization**: Is permission checked on EVERY action, not just at entry? (Horizontal & vertical privilege escalation)

### 5. Check Cryptography

Verify:

- **Uses vetted libraries**: OpenSSL, libsodium, NaCl (not custom crypto)
- **Authenticated encryption**: AES-GCM or ChaCha20-Poly1305 (not AES-CBC alone)
- **Key derivation**: Argon2 or PBKDF2 with high iteration count (not plain hashing)
- **Random generation**: Crypto-secure RNG (not `Math.random()` or `rand()`)
- **No hardcoded secrets**: Keys loaded from secure storage, environment variables, or key management service

### 6. Review Error Handling & Logging

Ensure:

- **No sensitive info in errors**: Error messages don't expose stack traces, SQL, API keys, or PII to users
- **Logging is secure**: Logs don't contain passwords, tokens, or sensitive data
- **Errors are logged**: Failed auth attempts, unauthorized access, data modifications logged
- **Log retention**: Logs stored securely; old logs rotated/deleted per compliance

## Output Format

A security review comment:

```markdown
## Security Review

### High-Severity Issues

- **A03 (Injection)**: SQL query uses string concatenation on line 45. Use parameterized query instead.
```

// Bad:
db.query("SELECT _ FROM users WHERE email = '" + email + "'")
// Good:
db.query("SELECT _ FROM users WHERE email = ?", [email])

```

### Medium-Severity Issues
- **A07 (Auth Failures)**: Login endpoint has no rate limiting. Attacker can brute-force passwords.
- Add rate limiting (e.g., max 5 attempts per 15 min per IP)

### Low-Severity Issues
- **A09 (Logging)**: Successful login not logged. Consider adding: `log.info("Login successful", {user_id, ip})`

### Approved
- CSRF token present on form submission
- Passwords hashed with bcrypt (good library, good practice)
```

## Worked Example

**Security Review: User Registration Feature**

```markdown
## Security Code Review: User Registration

### Critical Issues

1. **A02 (Cryptographic Failures)**: Password hashed with MD5 (line 78)
   - MD5 is broken; use bcrypt, Argon2, or PBKDF2
   - Current: `hash = md5(password)`
   - Fixed: `hash = bcrypt(password, salt_rounds=12)`

2. **A03 (Injection)**: Email confirmation link not validated (line 120)
   - Attacker can forge confirmation tokens
   - Current: `token = generate_random_string(6)` (too short, 10^6 combinations)
   - Fixed: `token = secrets.token_urlsafe(32)` (cryptographically secure, 2^256 space)

3. **A01 (Broken Access Control)**: Users can register with any email (no domain whitelist)
   - Decide: Should we whitelist email domains? Should we require verification before access?
   - Add: Email verification before account activation

### High-Severity Issues

4. **A07 (Auth Failures)**: Registration endpoint allows 100 requests/sec per IP
   - Add rate limiting: Max 5 registration attempts per minute per IP
   - Prevents brute-force email enumeration and bot attacks

5. **A09 (Logging)**: Failed registration attempts not logged
   - Add: `log.warn("Registration failed", {email, reason, ip})`

### Medium-Severity Issues

6. **A05 (Misconfiguration)**: Error message leaks whether email exists
   - Current: `"Email already registered"` vs. `"Invalid email"`
   - Fixed: Same message for both: `"If that email exists, a confirmation link has been sent"`
   - Prevents email enumeration

7. **A06 (Vulnerable Components)**: bcrypt library version 2.x (old)
   - Upgrade to 5.x: `npm update bcrypt`

### Approved

- HTTPS enforced (no http:// fallback)
- CSRF token on form; validated server-side
- Password field masked in UI; not logged server-side
- Email address validated (basic regex) before signup
```

---

## Decision Framework

When reviewing and facing ambiguity:

- **If input validation seems "strict enough"**: Ask "Can an attacker bypass this?" Whitelist is more secure than blacklist.
- **If error message leaks info**: Err on the side of caution. Generic error messages are safer.
- **If rate limiting is discussed**: Include it. Rate limiting is cheap; brute-force attacks are common.
- **If you see crypto code**: Ask an expert. Don't assume it's correct without review.
- **If a mitigating control is missing**: Don't mark as "nice-to-have." Flag it as an issue with clear guidance.

## Anti-Patterns & Guards

### Anti-Pattern 1: Reviewing Only for Logic

**Description**: Checking if code works, not if it's secure. Missing injection, auth, encryption flaws.

**Guard**: Security review is separate from functional review. Ask "What can an attacker do?" for every input/output.

### Anti-Pattern 2: Vague Findings

**Description**: "This code is insecure" without explaining why or how to fix it.

**Guard**: Every finding must have: (1) specific vulnerability, (2) attack scenario, (3) remediation code.

### Anti-Pattern 3: Over-Relying on Library

**Description**: "We use bcrypt so passwords are safe" without checking how it's used.

**Guard**: Even good libraries can be misused. Check: salt rounds, error handling, verification logic.

### Anti-Pattern 4: Ignoring Privilege Escalation

**Description**: Checking authentication but not authorization on every action.

**Guard**: Ask "Can a user access/modify data they shouldn't?" for every endpoint.

### Anti-Pattern 5: Not Documenting Accepted Risks

**Description**: Flagging an issue but not clarifying if it's a blocker or acceptable.

**Guard**: Clarify severity. Is it a "must fix before ship" or a "fix in next sprint"?

## Quality Checklist

Before approving code:

- [ ] **All input is validated**: Type, length, format, range checked
- [ ] **No SQL injection**: Parameterized queries used; no string concatenation
- [ ] **No XSS**: Output encoded for context (HTML, URL, JS)
- [ ] **Authentication is enforced**: Identity verified server-side
- [ ] **Authorization is enforced**: Permission checked on every action
- [ ] **Sensitive data encrypted**: At rest and in transit
- [ ] **Errors are safe**: No sensitive info leaked
- [ ] **Logging is comprehensive**: Failures and suspicious activity logged
- [ ] **Dependencies are current**: No known CVEs in libraries
- [ ] **Team alignment**: Security and engineering agree on findings and severity

## Further Reading

- OWASP Top 10 2021: https://owasp.org/Top10/
- OWASP Code Review Guide: https://owasp.org/www-project-code-review-guide/
- CWE Top 25: https://cwe.mitre.org/top25/
- Seacord, Robert C. _Secure Coding in C and C++_ (2nd ed.). Addison-Wesley, 2013.
- Stuttard, Dafydd, and Marcus Pinto. _The Web Application Hacker's Handbook_ (2nd ed.). Wiley, 2011.
