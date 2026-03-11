---
name: secrets-management
description: Manage API keys, credentials, and secrets securely using vaults, environment variables, and rotation policies. Prevent secrets from being committed to code or exposed in logs.
---

# Secrets Management

Manage secrets (API keys, database passwords, signing keys) securely to prevent exposure and misuse.

## Context

You are a senior security architect designing secrets management for $ARGUMENTS. Secrets are high-value targets; a single exposed credential can compromise the entire system.

## Domain Context

- **Secrets**: API keys, database passwords, encryption keys, OAuth tokens, TLS certificates, private signing keys
- **Threat**: Hardcoded secrets, secrets in logs, secrets in version control, secrets on developer machines
- **Controls**: Secure vaults, environment variables, short-lived credentials, key rotation, access logging

## Instructions

1. **Never Hardcode Secrets**:
   - No API keys, passwords, or private keys in source code
   - No secrets in configuration files checked into git
   - Audit git history for accidentally committed secrets (use `git-secrets`, `truffleHog`)
   - If found, revoke immediately and rotate

2. **Use Secure Vault**:
   - **HashiCorp Vault**: Centralized, flexible, supports dynamic secrets
   - **AWS Secrets Manager**: Managed, integrates with IAM, automatic rotation
   - **Azure Key Vault**: Microsoft-native, integrates with Entra ID
   - **Kubernetes Secrets**: For containerized deployments (note: base64-encoded, not encrypted by default)
   - Load secrets at runtime, not at build time

3. **Environment Variables** (for development):
   - Store secrets in `.env` files (never commit to git; add to `.gitignore`)
   - Load with `python-dotenv`, `go-dotenv`, or similar
   - In production, use managed secrets service instead

4. **Access Control**:
   - Principle of least privilege: Only services/users that need a secret can access it
   - Audit logging: Track all secret access (who, when, which secret)
   - Time-bound access: Temporary credentials for sensitive operations
   - MFA/approval required for sensitive secret access (e.g., production database password)

5. **Key Rotation**:
   - Rotate API keys annually or quarterly (NIST recommendation)
   - Rotate immediately after suspected compromise
   - **Rolling rotation**: Deploy new key, keep old key for grace period, then disable
   - Automatic rotation: Many managed services (AWS RDS, Google Cloud SQL) support automatic credential rotation

6. **Secrets in Logs**:
   - Configure logging to redact secrets (API keys, tokens, passwords)
   - Never log authentication headers or request bodies with credentials
   - Sanitize error messages that might leak secrets
   - Example regex for log redaction: `Authorization: Bearer [^,\s]*` → `Authorization: Bearer ***`

7. **Certificate Management**:
   - TLS certificates: Store private key in vault, not in version control
   - Rotate certificates before expiry (e.g., 30 days before)
   - Use ACME (Let's Encrypt) for automatic renewal
   - Monitor certificate expiry; alert if not renewed in time

## Anti-Patterns

- Storing secrets in environment variables on disk (`.env` files in production); **use managed secrets service**
- Using the same secret across environments (dev, staging, prod); **each environment should have separate, rotation-locked secrets**
- Never rotating secrets; **rotation is standard practice, not optional**
- Logging secrets (even "by accident"); **configure logging redaction; don't rely on developers to avoid logging secrets**
- Sharing secrets between services; **each service should have its own credentials with narrowly scoped permissions**

## Further Reading

- OWASP Secrets Management Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html
- HashiCorp Vault Documentation: https://www.vaultproject.io/docs
- AWS Secrets Manager Best Practices: https://docs.aws.amazon.com/secretsmanager/latest/userguide/best-practices.html
- NIST SP 800-57 (Key Management): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57Pt1r5.pdf
