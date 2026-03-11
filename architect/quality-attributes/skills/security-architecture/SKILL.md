---
name: security-architecture
description: Design security architecture covering authentication, authorization, data protection, and threat models. Use when building security-critical systems.
---

# Security Architecture

Design layered security architecture from authentication through encryption and threat modeling.

## Context

You are designing security for a system. The user handles sensitive data or faces regulatory requirements. Read their threat model and compliance needs.

## Domain Context

Based on OWASP, NIST, and zero-trust architecture principles:

- **Defense in Depth**: Multiple layers of security; one breach doesn't expose everything
- **Least Privilege**: Every component has minimum necessary permissions
- **Zero Trust**: Never trust, always verify; authenticate and authorize every request
- **Encryption in Transit & at Rest**: Prevent eavesdropping and unauthorized access
- **Audit Trails**: Every security-relevant action logged for forensics

## Instructions

1. **Threat Model**: Identify assets (data, functions), threats (unauthorized access, data leakage), and mitigations. Use STRIDE framework.

2. **Design Authentication**: Specify identity verification. Options: username/password (weakest), OAuth2 (better), mTLS (strongest). Support multi-factor authentication (MFA).

3. **Design Authorization**: Specify access control. Role-based access control (RBAC) or attribute-based (ABAC)? Who can read/write/delete which resources?

4. **Protect Data**: Data at rest: encrypt database and backups. Data in transit: use TLS 1.2+. Keys: use KMS (Key Management Service), never hardcode.

5. **Audit & Monitor**: Log all security-relevant actions. Monitor for suspicious patterns (brute force, unusual access patterns). Alert on threshold violations.

## Anti-Patterns

- **Security as Afterthought**: Build system, add security later. Result: pervasive vulnerabilities. **Guard**: Security architecture defined during design phase.
- **Assuming HTTPS is Enough**: Encrypt traffic but not database. Result: database breach exposes data. **Guard**: Encrypt data at rest independently of TLS.
- **Hardcoding Secrets**: API keys, passwords in code. Result: exposure in logs, backups, repositories. **Guard**: Use KMS or secret management service for all secrets.
- **No Audit Trail**: Can't investigate breaches. **Guard**: Log all auth, authz, and data access decisions. Immutable audit log.

## Further Reading

- _Threat Modeling_ by Adam Shostack — STRIDE framework and threat identification
- _Web Application Security_ by Andrew Hoffman — practical defense strategies
- _NIST Cybersecurity Framework_ — comprehensive security controls and maturity model
