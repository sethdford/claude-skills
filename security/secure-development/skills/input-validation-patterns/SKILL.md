---
name: input-validation-patterns
description: Design and implement input validation patterns (whitelisting, boundary checks, type validation) to prevent injection and buffer overflow attacks.
---

# Input Validation Patterns

Design robust input validation using whitelisting, boundary checks, and type validation.

## Context

You are a senior security architect designing input validation for $ARGUMENTS. Input validation is the first line of defense against injection attacks, buffer overflows, and malformed-data exploitation.

## Domain Context

- **Whitelisting vs. Blacklisting**: Whitelist allowed characters/patterns (safe-list approach); blacklisting is fragile and incomplete
- **Validation Points**: Validate at every trust boundary; don't assume data from database or internal APIs is safe
- **Canonicalization**: Normalize input (remove encoding, aliases) before validation (e.g., `../../etc/passwd` → `/etc/passwd`)
- **Type Safety**: Enforce data types (integer, email, UUID); avoid string representations that get misinterpreted

## Instructions

1. **Define Validation Rules** for each input:
   - **Type**: Integer, string, email, UUID, date, IP address, etc.
   - **Length**: Min and max length (prevents buffer overflow, DoS)
   - **Format**: Regex or pattern (email: `^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$`)
   - **Range**: Min/max value for numbers (e.g., age 0-150, quantity 1-1000)
   - **Allowed Characters**: Whitelist (e.g., for filename: alphanumeric, dash, underscore only)
   - **Business Rules**: Must be unique, must exist in reference table, must be in future, etc.

2. **Implement Whitelisting** (not blacklisting):

   ```
   Bad (blacklisting): Remove dangerous characters (always incomplete)
   input = input.replace("'", "").replace(";", "")

   Good (whitelisting): Accept only known-safe characters
   if (!preg_match('/^[a-zA-Z0-9_-]*$/', input)) { reject }
   ```

3. **Canonicalize Before Validation**:
   - URL-decode: `%2e%2e%2f` → `../`
   - HTML-decode: `&quot;` → `"`
   - Remove null bytes (legacy, but still relevant)
   - Normalize paths: resolve `..` and `.` before checking against allow-list

4. **Validate at Boundaries**:
   - User input from web forms → validate
   - API parameters → validate
   - Database queries (even if from trusted system) → prepare statements
   - File uploads → validate MIME type, size, content
   - Configuration files → validate before use

5. **Handle Validation Failures Securely**:
   - Reject invalid input; don't try to "fix" it
   - Log validation failures (don't expose to user)
   - Return generic error to user ("Invalid input")
   - Alert on repeated failures (possible attack)

## Anti-Patterns

- Blacklisting dangerous characters; **always use whitelisting**
- Trusting data from "internal" sources; **validate at every boundary**
- Validating format but not enforcing type safety; **"123" is a valid string but not a valid 32-bit integer if out of range**
- Performing validation in client-side only; **always validate server-side; client validation is for UX, not security**
- Trying to sanitize input for multiple contexts; **validate once, encode once per context (HTML context gets HTML encoding, SQL context gets parameterized queries, etc.)**

## Further Reading

- OWASP Input Validation Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html
- OWASP Deserialization Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Deserialization_Cheat_Sheet.html
- NIST SP 800-53 (SI-10 Information System Monitoring): Input validation requirements
- Semantic Exploitation (research on flaws in validation logic): https://cs.umass.edu/~amir/papers/semex.pdf
