---
name: certificate-management
description: Manage digital certificates for HTTPS, mutual TLS, code signing, and infrastructure security.
---

# Certificate Management

Manage digital certificates for TLS/HTTPS, mTLS, and code signing.

## Context

You are a senior infrastructure security engineer managing certificates for $ARGUMENTS. Certificates authenticate systems, encrypt communications, and sign code. Poor certificate management leads to data breaches (expired certificates, weak algorithms), service interruptions (undetected expirations), and trust violations (unauthorized CA-signed certificates).

## Domain Context

- **Certificate Types**: Self-signed (testing only), CA-signed (public trust), internal CA (enterprise)
- **Algorithms**: RSA (2048+ bits for legacy, 4096 for long-term), ECDSA (P-256 for modern applications)
- **Lifecycle**: Generation, installation, renewal (before expiration), revocation
- **Automation**: ACME (Automated Certificate Management Environment) for Let's Encrypt integration, auto-renewal
- **Compliance**: Certificates must meet compliance requirements (key size, algorithm, renewal intervals)

## Instructions

1. **Establish Certificate Authority (CA)**:
   - **Public CA**: Use for internet-facing services (Let's Encrypt free, DigiCert/Comodo commercial)
   - **Internal CA**: For internal services, testing; establish trusted root CA, intermediate CAs
   - **Self-Signed**: Only for testing/development; never production
   - **Key Management**: Private CA key stored in HSM (Hardware Security Module) or encrypted vault; access tightly controlled

2. **Implement HTTPS/TLS**:
   - **Certificate Acquisition**:
     - Public CA: Use Let's Encrypt (free, automated renewal) or commercial CA
     - Wildcard Certificates: `*.example.com` covers all subdomains
     - SANs (Subject Alternative Names): For multiple domains in one certificate
   - **TLS Configuration**:
     - TLS 1.2 minimum (1.3 preferred); disable TLS 1.0, 1.1
     - Strong cipher suites (ChaCha20-Poly1305, AES-256-GCM with forward secrecy)
     - HSTS header (enforce HTTPS redirects)
   - **Testing**: Use SSL Labs (sslabs.com) to verify TLS configuration

3. **Manage Certificate Lifecycle**:
   - **Inventory**: Maintain inventory of all certificates (domain, expiration, CA)
   - **Monitoring**: Alert 30/14/7 days before expiration; prevent accidental expirations
   - **Renewal**: Automate renewal (ACME client, CDN renewal)
   - **Installation**: Update servers with new certificate before old one expires
   - **Revocation**: If key compromised, revoke certificate; deploy new one immediately

4. **Implement Mutual TLS (mTLS)**:
   - **Server Certificate**: Signed by CA; presented to clients
   - **Client Certificate**: Signed by same CA; clients present to server
   - **Validation**: Both sides verify certificate chain and check certificate is not revoked
   - **Use Cases**: Service-to-service authentication, secure APIs, zero-trust networks
   - **Certificate Distribution**: Securely distribute client certificates to authorized clients

5. **Code Signing & Artifact Management**:
   - **Code Signing**: Sign application binaries with certificate; clients verify signature before execution
   - **Timestamp**: Include timestamp in signature (certificate can expire, but signature remains valid if timestamped)
   - **Revocation**: Revoke certificate if key compromised; new versions must be signed with new certificate
   - **Artifact Repository**: Store certificates in secure vault; protect private keys

## Anti-Patterns

- Using self-signed certificates in production; **users see warnings; trust is compromised**
- Weak key sizes (RSA 1024, 512); **brute-forceable; use 2048+ RSA or ECDSA P-256+**
- Using TLS 1.0 or 1.1; **known vulnerabilities (POODLE, BEAST); use 1.2+**
- Manual renewal (human remembers to renew); **automate with ACME or CDN renewal**
- Not monitoring certificate expiration; **unexpected outages when certificate expires**

## Further Reading

- Let's Encrypt: https://letsencrypt.org/
- RFC 5246 (TLS 1.2): https://tools.ietf.org/html/rfc5246
- RFC 8446 (TLS 1.3): https://tools.ietf.org/html/rfc8446
- NIST SP 800-53 (Certificate Management): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf
- SSL Labs: https://www.ssllabs.com/ssltest/ (Test your TLS configuration)
