# Example: STRIDE Analysis for Freelancer Project Sharing Feature

## System Overview

**System Name**: Project Invite & Permissions System (for Freelancer Marketplace)

**Description**: Feature allows freelancers to invite clients to a project workspace. Clients can view project files, updates, and billing, but permissions are granular (view-only, comment, edit).

**Scope**:

- In scope: Invite mechanism, permission checks, role-based access control
- Out of scope: File storage encryption (handled by separate system), client authentication (SSO/SAML)

---

## Data Flow Diagram

```
Freelancer Web App
       ↓
       → [Invite Service]
           ↓
         [Database: Invites]
         [Database: Permissions]
           ↓
       ← [Permission Check]
           ↓
Client Web App
       ↓
[File Storage API]
[Billing API]
```

**Trust Boundaries**:

- Public internet ↔ Application server
- Application server ↔ Database

---

## Threat Analysis by STRIDE Category

### S - Spoofing Identity

| Threat                                                                        | Asset                      | Likelihood | Impact   | Mitigation                                                                                                                    |
| ----------------------------------------------------------------------------- | -------------------------- | ---------- | -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Attacker forges invite link and access project as fake client                 | Project data, billing info | Medium     | High     | Use cryptographically random invite tokens (UUID v4); expire after 7 days or first use; verify token integrity with HMAC      |
| Freelancer impersonates another freelancer to invite someone to their project | Project data               | Low        | High     | Verify freelancer ownership before allowing invite; check freelancer ID matches project owner                                 |
| Client brute-forces invite link to guess other projects                       | Multiple projects          | Medium     | Critical | Rate-limit invite endpoint (10 requests/min/IP); implement exponential backoff after failed attempts; log all failed attempts |

---

### T - Tampering with Data

| Threat                                                                                  | Asset                       | Likelihood | Impact   | Mitigation                                                                                                                            |
| --------------------------------------------------------------------------------------- | --------------------------- | ---------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Attacker modifies invite to grant higher privileges (view-only → admin)                 | Permissions, project access | Low        | Critical | Sign invites with HMAC-SHA256; verify signature before processing; store permissions in database (not in invite token)                |
| Client intercepts and modifies permission string in API call (role: "viewer" → "admin") | Permissions                 | Medium     | High     | Validate all permission changes server-side; don't trust client-submitted permissions; enforce role hierarchy; log permission changes |
| Attacker changes their own role after invitation accepted                               | Permissions                 | Medium     | High     | Permission checks must happen server-side on every API call; no client-side permission checks; use role claim from signed JWT         |

---

### R - Repudiation

| Threat                                                                     | Asset                              | Likelihood | Impact | Mitigation                                                                                                                                             |
| -------------------------------------------------------------------------- | ---------------------------------- | ---------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Client denies they accepted project invite; claims access was unauthorized | Project data access, audit trail   | Low        | Medium | Log all invite acceptance events (timestamp, IP, user agent); require explicit accept action; email confirmation of acceptance; retain logs for 1 year |
| Freelancer claims they didn't remove client's access (removes then denies) | Project permissions, client access | Low        | Medium | Immutable audit log of all permission changes (created, modified, revoked); log who made change and when; client receives email on removal             |

---

### I - Information Disclosure

| Threat                                                                                                   | Asset                                   | Likelihood | Impact   | Mitigation                                                                                                                                                   |
| -------------------------------------------------------------------------------------------------------- | --------------------------------------- | ---------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Invite token leaked in logs or error messages; attacker uses to access project                           | Project data                            | Medium     | Critical | Never log full invite tokens; log only first 8 chars; don't expose tokens in error messages; sanitize stack traces in production                             |
| Client email exposed in invite link or API response; attacker learns which clients use which freelancers | Client identity, privacy                | Medium     | Medium   | Use invite tokens instead of email addresses in URLs; don't return client email in API responses unless authenticated; encrypt email in transit (HTTPS only) |
| Attacker enumerates projects by guessing project IDs                                                     | Project existence, client relationships | High       | Medium   | Use UUID (not sequential IDs) for project IDs; don't expose project IDs in API; require authentication for all project endpoints                             |
| Permission checks bypass; client can see other projects they shouldn't                                   | Project data, privacy                   | Low        | Critical | Check user permissions on every API call; whitelist allowed actions; default to deny; test permission checks with automated security tests                   |

---

### D - Denial of Service

| Threat                                                                         | Asset                | Likelihood | Impact | Mitigation                                                                                                                   |
| ------------------------------------------------------------------------------ | -------------------- | ---------- | ------ | ---------------------------------------------------------------------------------------------------------------------------- |
| Attacker sends millions of invite requests; overloads service                  | Service availability | Medium     | High   | Rate limit: 100 invites/hour per freelancer; queue requests; implement circuit breaker for overload; monitor queue depth     |
| Attacker brute-forces permission endpoint; kills service with invalid requests | Service availability | Medium     | High   | Rate limit: 1000 API calls/hour per user; implement exponential backoff (10s, 100s, 1000s); block for 1 hour after threshold |
| Attacker creates massive invite list; database query slow                      | Service performance  | Low        | Medium | Index permission queries (user_id, project_id); paginate results; cache permission checks (5-min TTL)                        |

---

### E - Elevation of Privilege

| Threat                                                                                                | Asset                           | Likelihood | Impact   | Mitigation                                                                                                                          |
| ----------------------------------------------------------------------------------------------------- | ------------------------------- | ---------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Client with "viewer" role tricks API to grant themselves "editor" role                                | Project edit access             | Low        | Critical | No client-side role selection; server always determines role based on invite; reject API calls with role claims from client         |
| Freelancer with "editor" role grants themselves "admin" on someone else's project                     | Admin access, project ownership | Low        | Critical | Check freelancer owns project before allowing role changes; only project owner can grant admin; log all admin actions               |
| Attacker discovers permission API; calls it directly to assign themselves "editor" on random projects | Unauthorized access             | Medium     | Critical | Implement CSRF tokens on all state-changing endpoints; verify request origin; require authentication with valid session; rate limit |

---

## Risk Summary

| Threat ID | Threat Name                   | Category | Severity | Status |
| --------- | ----------------------------- | -------- | -------- | ------ |
| S-1       | Invite link forgery           | S        | Critical | New    |
| S-2       | Freelancer impersonation      | S        | Critical | New    |
| S-3       | Invite brute-force            | S        | Critical | New    |
| T-1       | Invite tampering              | T        | Critical | New    |
| T-2       | Permission escalation via API | T        | Critical | New    |
| T-3       | Client modifies own role      | T        | Critical | New    |
| R-1       | Repudiation of acceptance     | R        | Medium   | New    |
| R-2       | Repudiation of removal        | R        | Medium   | New    |
| I-1       | Token in logs                 | I        | Critical | New    |
| I-2       | Email exposure                | I        | Medium   | New    |
| I-3       | Project enumeration           | I        | Medium   | New    |
| I-4       | Permission bypass             | I        | Critical | New    |
| D-1       | Invite spam DoS               | D        | High     | New    |
| D-2       | API brute-force DoS           | D        | High     | New    |
| D-3       | Slow queries                  | D        | Medium   | New    |
| E-1       | Client role elevation         | E        | Critical | New    |
| E-2       | Freelancer admin escalation   | E        | Critical | New    |
| E-3       | Unauthorized permission API   | E        | Critical | New    |

---

## Mitigation Roadmap

### Phase 1 (Next 30 days): Critical Issues

- Implement HMAC signing for invite tokens (S-1, T-1)
- Add server-side permission validation (T-2, E-1)
- Implement rate limiting on invite & permission endpoints (S-3, D-1, D-2)
- Sanitize token logging (I-1)
- Add CSRF protection (E-3)

**Success Criteria**: All Critical-severity threats have mitigations in place; tests added for each mitigation

### Phase 2 (Next 90 days): High Severity + Audit

- Add audit logging for invite/permission changes (R-1, R-2)
- Implement permission query caching (D-3)
- Automated security tests for permission checks
- User education: how invites work, what permissions mean
- Penetration test by external firm

### Phase 3 (Next 6 months): Hardening + Monitoring

- Real-time alerting for permission anomalies
- Monthly threat review and update
- Customer communication about security features
- Consider implementing invite verification codes (SMS/email confirmation)

---

## Implementation Notes

### Development Checklist

- [ ] Generate invites as `secrets.token_urlsafe(32)` (cryptographically secure)
- [ ] Store hash of token in database: `hashlib.sha256(token.encode()).hexdigest()`
- [ ] Expire tokens: 7 days or on first use
- [ ] All permission checks server-side: `if not user_has_permission(user_id, project_id, 'edit'): return 403`
- [ ] Audit logging on every permission change: log timestamp, user, action, old value, new value
- [ ] Rate limiting: implement with Redis + sliding window
- [ ] CSRF protection: `flask-wtf` or equivalent; validate X-CSRF-Token
- [ ] Logging: never log full tokens, only first 8 chars
- [ ] Tests: 100+ test cases covering permission boundaries, role escalation attempts, expired tokens

### Testing Plan

- **Unit tests**: Permission check logic (pass/fail for each role)
- **Integration tests**: Full invite flow (freelancer invite → client accept → access check)
- **Security tests**: Attempt role escalation, token forgery, brute-force
- **Load tests**: Invite endpoint under 10K requests/min

---

## Review & Sign-Off

| Role             | Name   | Date   | Sign-Off |
| ---------------- | ------ | ------ | -------- |
| Security Lead    | [Name] | [Date] | [ ]      |
| Product Owner    | [Name] | [Date] | [ ]      |
| Engineering Lead | [Name] | [Date] | [ ]      |

---

## Next Steps

1. **Implement Phase 1 mitigations** (assign by end of week)
2. **Schedule security review** with team (45 min)
3. **Add threat tests to CI/CD** (ensure no regression)
4. **Plan external pentest** for Phase 2
5. **Communicate with customers** (security feature release notes)
