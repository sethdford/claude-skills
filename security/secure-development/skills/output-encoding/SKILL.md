---
name: output-encoding
description: Implement context-specific output encoding to prevent XSS and injection attacks. Encode HTML, URL, JavaScript, and other contexts appropriately.
---

# Output Encoding

Encode output based on context (HTML, URL, JavaScript, etc.) to prevent injection attacks.

## Context

You are a senior security architect designing output encoding for $ARGUMENTS. Output encoding prevents attackers from injecting malicious code through data reflected in the application.

## Domain Context

- **Context Matters**: HTML encoding ≠ URL encoding ≠ JavaScript encoding; use the right encoding for the context
- **Defense in Depth**: Validation prevents bad input; encoding prevents bad output from being executed
- **Double Encoding Risk**: Don't double-encode (encode then encode again); decode once, encode once per context

## Instructions

1. **HTML Context** (most common):
   - `<` → `&lt;`
   - `>` → `&gt;`
   - `&` → `&amp;`
   - `"` → `&quot;`
   - `'` → `&#x27;`
   - Example: `<script>alert('xss')</script>` → `&lt;script&gt;alert(&#x27;xss&#x27;)&lt;/script&gt;`

2. **URL Context**:
   - Encode special characters: space → `%20`, `&` → `%26`, `?` → `%3F`
   - Use URL-safe encoding (percent-encoding/RFC 3986)
   - Example: `redirect=http://evil.com?a=1&b=2` → `redirect=http%3A%2F%2Fevil.com%3Fa%3D1%26b%3D2`

3. **JavaScript Context**:
   - Escape quotes: `'` → `\'`, `"` → `\"`
   - Escape backslashes: `\` → `\\`
   - Avoid dynamic code generation with untrusted input (instead use JSON and JSON.parse)
   - Example: data passed to JavaScript should be JSON-encoded, then parsed safely

4. **CSS Context**:
   - Escape special characters: newline, quote, backslash
   - Avoid using `expression()` or `-moz-binding` (older browsers)
   - Example: `color: user_input;` with `input = "red; background:url(evil.jpg)"` requires encoding

5. **Use Templating Engines with Auto-Encoding**:
   - Modern frameworks (React, Vue, Angular, Django, Jinja2) auto-escape HTML by default
   - Understand when auto-escaping is disabled (raw/unescape filters) and use only when necessary
   - Never disable auto-escaping globally; only for specific trusted data

## Anti-Patterns

- Relying on client-side encoding; **always encode server-side**
- Encoding in the wrong context; **HTML encoding is not URL safe; don't reuse encodings**
- Double-encoding; **if data is already JSON-encoded, don't HTML-encode it again**
- Trusting "frameworks handle it"; **verify auto-escaping is enabled; some template engines have it disabled by default**
- Encoding user input instead of output; **validate input, encode output; these are separate concerns**

## Further Reading

- OWASP XSS Prevention Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html
- HTML5 Security Cheatsheet: https://html5sec.org/
- OWASP Testing Guide (XSS): https://owasp.org/www-project-web-security-testing-guide/
