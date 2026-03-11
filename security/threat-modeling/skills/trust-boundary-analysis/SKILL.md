---
name: trust-boundary-analysis
description: Identify trust boundaries in system architecture where privilege levels, authority, or security contexts change. Use when designing authentication, authorization, and inter-component communication.
---

# Trust Boundary Analysis

Identify and document trust boundaries where privilege levels, security contexts, or threat models change.

## Context

You are a senior security architect analyzing trust boundaries for $ARGUMENTS. Trust boundaries are critical: threats are most likely to cross them, and controls must enforce privilege/authority at boundaries.

## Domain Context

- **Trust Boundary**: A line in an architecture where one side has fewer privileges or security assumptions than the other; threats are most likely here
- **Examples**: Frontend/Backend, Microservice A/B, Application/Database, User/Admin, Internal/External network, Untrusted Input/Processing
- **Control Points**: Authentication (verify identity), Authorization (enforce privileges), Encryption (confidentiality across network), Integrity (signatures/MACs for data crossing boundaries)
- **Implicit vs. Explicit**: Explicit boundaries are well-documented; implicit boundaries (e.g., "we trust library X") are risks waiting to happen

## Instructions

1. **Map Trust Zones**: Identify distinct security zones based on ownership, privilege level, or threat model. Examples:
   - **External Zone**: Untrusted users, unencrypted networks, no assumed privacy
   - **DMZ**: Web tier, exposed APIs, medium trust
   - **Internal Zone**: Backend services, database servers, higher trust (but still verify!)
   - **Admin Zone**: Super-user access, audit logging, strict controls

2. **Identify Boundaries**: Mark the lines where data crosses from one zone to another.

3. **For Each Boundary, Document**:
   - **Authentication**: How is identity verified? (API key, JWT, OAuth, mTLS)
   - **Authorization**: How are privileges enforced? (ACLs, role-based, capability-based)
   - **Encryption**: Is data encrypted in transit? At rest? (TLS, AES-GCM)
   - **Integrity**: How is data verified as unmodified? (signatures, HMACs)
   - **Logging/Audit**: Are boundary crossings logged and monitored?
   - **Error Handling**: Do error messages leak information across the boundary?

4. **Assess Threats at Boundaries**: For each boundary, ask:
   - Can an attacker impersonate a trusted party? (spoofing)
   - Can they intercept and modify data? (tampering)
   - Can they escalate privilege? (elevation)
   - Can they exfiltrate data? (disclosure)

5. **Design Controls**: Specify controls for each boundary based on sensitivity and attack likelihood.

## Anti-Patterns

- Assuming internal networks are trusted; **segment internal zones; a compromised internal service can pivot to others**
- Creating trust boundaries only at the network edge; **trust boundaries also exist between application processes, microservices, and privilege levels**
- Treating all boundaries equally; **a boundary crossing unprivileged user input requires stronger controls than a boundary between two internal services with mTLS**
- Documenting boundaries without enforcement mechanisms; **listing "we trust Service A" is not a control; specifying "mTLS + mutual authentication + audit logging" is**
- Forgetting implicit boundaries; **even if not drawn on a diagram, privilege transitions (user→app→database, frontend→API→backend) are trust boundaries**

## Further Reading

- Saltzer & Schroeder (1975). The Protection of Information in Computer Systems. (foundational principle: "complete mediation")
- Zero Trust Security Model: https://www.nist.gov/publications/zero-trust-architecture (NIST SP 800-207)
- Schneier, B. Secrets and Lies. (Chapter on security perimeters and why they don't work as assumed)
- OWASP: Authorization Cheat Sheet (enforcing privilege at boundaries)
