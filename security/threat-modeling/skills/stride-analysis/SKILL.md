---
name: stride-analysis
description: Systematically identify and document threats using the STRIDE framework (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege). Use when designing systems, reviewing architectures, conducting security design reviews, or updating threat models.
allowed-tools: Read, Grep, Glob, Write, Edit
---

# STRIDE Threat Modeling

Conduct a systematic threat analysis of a system's architecture using Microsoft's STRIDE framework to identify vulnerabilities before they're exploited.

## Context

You are a security architect helping a team identify threats in their system design. STRIDE is a structured approach that ensures comprehensive coverage across six threat categories. Unlike ad-hoc "security brainstorming," STRIDE forces you to ask the right questions for each component and data flow, ensuring threats aren't missed.

Done well, threat modeling catches design flaws early (when they're cheap to fix). Done poorly (checklist-style, without understanding), it generates noise and wastes engineering time.

## Domain Context

- **STRIDE Framework (Microsoft)**: Six threat categories that map to security properties:
  - **Spoofing (Identity)**: Can attackers impersonate a user, service, or component?
  - **Tampering (Integrity)**: Can attackers modify data in transit or at rest?
  - **Repudiation (Accountability)**: Can actors deny their actions? Are audit trails protected?
  - **Information Disclosure (Confidentiality)**: Can unauthorized parties access sensitive data?
  - **Denial of Service (Availability)**: Can attackers degrade or crash services?
  - **Elevation of Privilege (Authorization)**: Can attackers gain higher-privilege access than intended?
- **Trust Boundaries**: Foundational concept—threats cross boundaries; within boundaries, assume trust
- **Data Flow Diagrams (DFD)**: Map components, actors, and data flows before analyzing threats
- **Threat Severity**: Likelihood × Impact (critical, high, medium, low)
- **Mitigations**: Controls that reduce threat severity (preventive, detective, compensating)

## When to Use This Skill

- You're designing a new system or major architectural change and want to identify threats early
- You're conducting a security design review before engineering starts
- You need to document threats for audit/compliance purposes
- You're updating your threat model based on new features or architecture changes
- A security researcher or customer asks "Have you done threat modeling?"

## Prerequisites

Before starting STRIDE analysis, gather:

1. **System architecture**: Diagrams showing components, data flows, external systems, trust boundaries
2. **Authentication/authorization model**: How are users/services identified and authorized?
3. **Data classification**: What data is sensitive (PII, financial, healthcare)? Where is it stored and transmitted?
4. **Existing controls**: What security measures already exist (encryption, logging, firewalls)?
5. **Compliance context**: Are there regulatory requirements (PCI-DSS, HIPAA, SOC2) that drive threat severity?

If documentation is missing, start by drawing the architecture with the team.

## Instructions

### 1. Map Components & Data Flows

Create or review a Data Flow Diagram (DFD) showing:

- **External entities** (users, APIs, partners)
- **Processes** (application, microservices, functions)
- **Data stores** (databases, caches, logs)
- **Data flows** (APIs, network calls, database queries)
- **Trust boundaries** (where privilege/trust levels change)

Example:

```
[User] --HTTPS--> [Web App] --SQL--> [Database]
                      |
                   [API Log]
                      |
                 [SIEM/Alert]

Trust boundary: Outside | Web App Layer | Database Layer
```

### 2. For Each Component, Apply STRIDE

For each process, data store, or data flow, systematically ask:

**Spoofing (Identity)** questions:

- Can someone impersonate this component/user?
- How is identity verified (authentication)?
- Can credentials be stolen or replayed?
- Is multi-factor authentication enforced?

**Tampering (Integrity)** questions:

- Can data be modified in transit (man-in-the-middle)?
- Can data be modified at rest (database compromise)?
- Is data integrity checked (signatures, hashes)?
- Are there version controls or audit trails?

**Repudiation (Accountability)** questions:

- Can actors deny their actions?
- Are actions logged?
- Are logs protected from tampering?
- Can logs be correlated across systems?

**Information Disclosure (Confidentiality)** questions:

- Is data encrypted in transit (HTTPS, TLS)?
- Is data encrypted at rest?
- Who has access to this data?
- Can data be extracted (logging, debugging, sidechannels)?

**Denial of Service (Availability)** questions:

- Can attackers consume resources (CPU, disk, memory)?
- Can service be crashed or rate-limited?
- Are there recovery mechanisms?
- Is capacity planning done?

**Elevation of Privilege (Authorization)** questions:

- Can users exceed their intended permissions?
- Is authorization checked on every action (not just at entry)?
- Are roles/permissions clearly defined?
- Are there administrative backdoors or emergency access?

### 3. Document Threats

For each threat, document:

- **ID**: Unique identifier (T1, T2, etc.)
- **Category**: STRIDE category
- **Component**: What's being threatened (e.g., "API-Database connection")
- **Threat**: Specific attack scenario (e.g., "Attacker executes SQL injection to extract user records")
- **Severity**: Critical/High/Medium/Low based on likelihood and impact
- **Existing Controls**: What's already protecting against this
- **Mitigation**: Recommended control (preventive or detective)
- **Status**: Open/Mitigated/Accepted

### 4. Assign Severity

Severity = Likelihood × Impact

| Likelihood      | Impact                               | Severity     |
| --------------- | ------------------------------------ | ------------ |
| High (>50%)     | Critical (customer data, downtime)   | **CRITICAL** |
| High            | High (service disruption, data loss) | **HIGH**     |
| Medium (10-50%) | Critical                             | **HIGH**     |
| Medium          | High                                 | **MEDIUM**   |
| Low (<10%)      | Critical                             | **MEDIUM**   |
| Low             | High                                 | **LOW**      |
| Low             | Medium (minor disruption)            | **LOW**      |

### 5. Link to Mitigations

Match each threat to:

- **Preventive controls**: Stop the threat (e.g., encryption prevents eavesdropping)
- **Detective controls**: Detect the attack (e.g., logs detect unauthorized access)
- **Compensating controls**: Reduce impact if attack succeeds (e.g., backup restores data)

### 6. Review & Prioritize

Prioritize mitigations by:

1. Critical & unmitigated threats first
2. High threats with feasible mitigations
3. Medium threats with low effort
4. Accept low-severity risks (documented decision)

## Output Format

A STRIDE Threat Model document:

```
# STRIDE Threat Model: [System Name]

## System Overview
[Brief architecture description, DFD, trust boundaries]

## Threat Analysis

| ID | Category | Component | Threat | Severity | Existing Controls | Mitigation | Status |
|----|----------|-----------|--------|----------|-------------------|-----------|--------|
| T1 | Spoofing | API Auth | Attacker replays valid JWT | High | JWT signed, TTL 1hr | Rate limit auth failures | Open |
| T2 | Tampering | DB Connection | MITM modifies SQL queries | Critical | No TLS | Enforce TLS 1.2+ | Open |
| T3 | Information Disclosure | Logs | Sensitive data logged | High | No log encryption | Redact PII in logs | Open |

## Critical Findings Summary
- [List critical/high threats needing immediate attention]

## Mitigations Roadmap
- [Phase 1]: [Mitigations for critical threats]
- [Phase 2]: [Mitigations for high threats]

## Accepted Risks
- [Threats accepted with business justification and timeline to mitigate]
```

## Worked Example

**STRIDE Threat Model: Freelancer Project Sharing Feature**

## System Overview

Users share project links (one-click, read-only) with clients. Shared link grants read-only access to project files via a public URL (no authentication required).

```
[Client] --HTTP(S)--> [Web App] --[Token Lookup]--> [Database]
                          |
                      [File Storage]

Trust Boundary: Unauthenticated | Web App | Private Systems
```

| ID  | Category               | Component    | Threat                                           | Severity | Existing Controls                 | Mitigation                                           | Status |
| --- | ---------------------- | ------------ | ------------------------------------------------ | -------- | --------------------------------- | ---------------------------------------------------- | ------ |
| T1  | Spoofing               | Shared Link  | Attacker guesses valid token                     | Medium   | Tokens 32 bytes entropy, URL-safe | Use cryptographic PRNG (not Math.random)             | Open   |
| T2  | Information Disclosure | Shared Link  | Token leaked in browser history, referrer header | High     | HTTPS only, no query params       | Put token in POST body or use signed URLs            | Open   |
| T3  | Tampering              | Shared Link  | Attacker modifies token to access other projects | High     | Cryptographically signed tokens   | Use authenticated encryption (HMAC-SHA256)           | Open   |
| T4  | Denial of Service      | Shared Link  | Attacker floods requests to exhaust capacity     | Medium   | CloudFront caching                | Rate limit by IP; implement CAPTCHA                  | Open   |
| T5  | Information Disclosure | File Storage | Project files stored unencrypted                 | Critical | Files at rest unencrypted         | Encrypt files at rest (AES-256)                      | Open   |
| T6  | Elevation of Privilege | Shared Link  | Attacker modifies token to grant edit access     | Critical | Read-only token checks API        | Enforce read-only at every API call (not just auth)  | Open   |
| T7  | Repudiation            | Audit Log    | Attacker accesses project without audit trail    | High     | No audit logging                  | Log all shared link accesses (who, when, what files) | Open   |

**Critical Findings**:

- T5: Files stored unencrypted at rest (CRITICAL)
- T6: Read-only enforcement only at auth layer, not per-request (CRITICAL)

**Mitigations Roadmap**:

- **Phase 1** (Week 1): Implement authenticated token signing (HMAC); enforce read-only at every file access
- **Phase 2** (Week 2): Encrypt files at rest (AES-256); add audit logging for shared link access
- **Phase 3** (Week 3): Add rate limiting per IP; implement CAPTCHA on brute-force attempts

---

## Decision Framework

When analyzing threats and facing ambiguity:

- **If a threat feels too generic** ("Someone could hack it"): Make it specific. What component? What's the attack path? What data is at risk?
- **If you're not sure about Likelihood**: Ask "Has this been exploited before?" or "How many attack steps does this take?" More steps = lower likelihood.
- **If Impact is unclear**: Ask "If this happens, what's lost?" Data? Service uptime? Compliance? Quantify in business terms.
- **If you can't articulate a mitigation**: The threat might be accepted (with documented risk). Don't list "security review" as a mitigation (too vague).
- **If a threat is cross-cutting (e.g., "encrypt all data")**: Break it into component-specific mitigations (DB encryption, TLS, log encryption).

## Anti-Patterns & Guards

### Anti-Pattern 1: Threat Listing Without Context

**Description**: "Spoofing threat" for every component; no specific attack scenario.

**Guard**: Every threat must answer: "Attacker does X to [component] to achieve Y." If you can't fill in X and Y, it's not a threat; it's a buzzword.

### Anti-Pattern 2: Ignoring Insider Threats

**Description**: Threat model assumes all insiders are trusted; focuses only on external attackers.

**Guard**: Ask "What could a disgruntled employee do?" Insider threats are real and often have high impact.

### Anti-Pattern 3: Vague Mitigations

**Description**: "Use encryption" without specifying where, how, or what algorithm.

**Guard**: Mitigations must be specific. "Encrypt PII at rest using AES-256 with key rotation every 90 days" is actionable.

### Anti-Pattern 4: Not Revisiting After Architecture Changes

**Description**: STRIDE done once; never updated when architecture changes.

**Guard**: Threat model is living document. Update when adding features, changing platforms, or after security incidents.

### Anti-Pattern 5: All Threats Marked "Critical"

**Description**: Over-inflating severity to make everything seem urgent.

**Guard**: If everything is critical, nothing is. Severity must differentiate; justify why each threat has its rating.

## Quality Checklist

Before sharing the threat model:

- [ ] **All components analyzed**: Every process, data store, and data flow has been examined for STRIDE threats
- [ ] **Threats are specific**: Each threat has a concrete attack scenario, not generic language
- [ ] **Severity is defensible**: Likelihood and impact are justified (backed by evidence or reasoning)
- [ ] **Mitigations are actionable**: Each mitigation is specific; engineers know what to build
- [ ] **Controls are mapped**: Existing controls are documented; gaps are clear
- [ ] **Insider threats included**: Model considers threats from employees, not just external attackers
- [ ] **Trust boundaries clear**: Where privilege/trust changes are explicit
- [ ] **Team reviewed**: Security and engineering reviewed together; disagreements noted

## Further Reading

- Microsoft STRIDE per Element: https://learn.microsoft.com/en-us/windows-hardware/drivers/drm/threat-modeling-documentation
- Shostack, Adam. _Threat Modeling: Design for Security_. Wiley, 2014. Comprehensive guide to STRIDE and DFD-based threat modeling.
- NIST SP 800-30: Risk Assessment guidance for threat severity and likelihood calibration.
- OWASP Threat Dragon: Free tool for creating DFDs and threat models.
- BSA Framework Threat Modeling Playbook: Step-by-step playbook with examples.
