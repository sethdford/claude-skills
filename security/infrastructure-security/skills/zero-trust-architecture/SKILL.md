---
name: zero-trust-architecture
description: Design and implement zero-trust architecture to authenticate and authorize all access, eliminating trust based on location.
---

# Zero-Trust Architecture

Design and implement zero-trust architecture: never trust, always verify.

## Context

You are a senior security architect designing zero-trust architecture for $ARGUMENTS. Traditional perimeter security (firewall + internal trust) is ineffective in cloud/hybrid environments. Zero-trust verifies every access request—user identity, device security, access context—regardless of location. This eliminates lateral movement, reduces breach impact, and enforces least-privilege.

## Domain Context

- **Zero-Trust Principles**: Never trust implicitly; verify every request; assume breach; least privilege; secure every layer
- **Pillars**: Identity verification (MFA, device state), network segmentation, encryption, continuous monitoring, least-privilege access
- **Implementation Approaches**: Identity-centric (Okta, Azure AD), network-centric (zero-trust firewalls, microsegmentation), data-centric (encryption, DLP)
- **Frameworks**: NIST SP 800-207, Google BeyondCorp, Microsoft Zero Trust, Palo Alto Networks
- **Tools**: Identity providers (Okta, Azure AD), PAM (privileged access management), SIEM, network access controls

## Instructions

1. **Establish Identity Verification**:
   - **User Identity**: Strong authentication (MFA required); no password-only access
     - MFA options: TOTP, hardware tokens (YubiKey), biometric, Push notifications (out-of-band)
   - **Device Identity**: Verify device is trusted (OS up-to-date, antivirus enabled, disk encryption)
   - **Service Identity**: Services authenticate to each other (mTLS, signed tokens, service accounts)
   - **Continuous Verification**: Re-verify during session (not just at login); detect compromised credentials

2. **Implement Network Segmentation & Microsegmentation**:
   - **Zero-Trust Firewalls**: Enforce rules at application layer (not just IP/port)
     - Deny by default; explicitly allow only needed access
     - Rules based on identity, device state, network context (location, time)
   - **Microsegmentation**: Isolate workloads; pod-to-pod, server-to-server traffic controlled
   - **Encrypted Tunnels**: All internal traffic encrypted (east-west encryption)

3. **Enforce Least-Privilege Access**:
   - **Just-In-Time (JIT) Access**: Grant temporary access (1-4 hours) only when needed
   - **Just-Enough-Privilege (JEP)**: Grant minimum permissions for task
   - **Conditional Access**: Access rules based on conditions (time, device, location, network)
   - **Privileged Access Management (PAM)**: Separate admin accounts; session recording; audit all admin actions
   - **Regular Reviews**: Quarterly audit of access; remove unnecessary permissions

4. **Continuous Monitoring & Anomaly Detection**:
   - **Behavioral Analytics**: Establish baseline user behavior (normal access patterns)
     - Alert on deviations: accessing unusual resources, unusual time, unusual location, bulk downloads
   - **Event Logging**: Log all authentication, authorization, data access; immutable logs
   - **Threat Detection**: Use SIEM to correlate events; detect attack chains
   - **Rapid Response**: Automated response to detected threats (revoke access, trigger MFA, quarantine device)

5. **Encrypt Everything**:
   - **Data in Transit**: TLS 1.2+ for all external; mTLS for internal services
   - **Data at Rest**: Encryption at database, storage, backup levels
   - **Key Management**: Centralized key management (AWS KMS, HashiCorp Vault); separate keys per purpose
   - **Encryption Protocols**: AES-256 for symmetric, RSA/ECDSA for asymmetric, Argon2 for passwords

## Anti-Patterns

- Assuming internal traffic is trusted; **encrypt and verify all traffic**
- Network-only segmentation without identity verification; **attackers compromise user credentials; verify identity, not just network**
- Long-lived access tokens; **short-lived tokens (hours/minutes) reduce compromise window**
- No monitoring; **you won't detect breaches; continuous monitoring essential**
- Treating zero-trust as binary ("we're zero-trust"); **zero-trust is maturity model; continually improve**

## Further Reading

- NIST SP 800-207 (Zero Trust Architecture): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-207.pdf
- Google BeyondCorp: https://cloud.google.com/beyondcorp/
- Microsoft Zero Trust: https://www.microsoft.com/en-us/security/zero-trust/
- Palo Alto Networks Zero Trust: https://www.paloaltonetworks.com/security-101/what-is-zero-trust
