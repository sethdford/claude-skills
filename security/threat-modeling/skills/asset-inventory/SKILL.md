---
name: asset-inventory
description: Create a comprehensive inventory of assets (data, systems, infrastructure, people) and their criticality, value, and dependencies. Use when prioritizing threats and allocating security resources.
---

# Asset Inventory

Document all critical assets, their value, sensitivity, and dependencies to understand what needs protection.

## Context

You are a senior security architect creating an asset inventory for $ARGUMENTS. Asset inventory is the foundation of threat modeling and risk assessment—you can't assess risk to what you haven't enumerated.

## Domain Context

- **Asset Types**: Data (PII, financial records, IP), Systems (servers, APIs, applications), Infrastructure (networks, databases), Credentials/Secrets (keys, tokens, passwords), People (employees, admins, contractors)
- **Valuation**: Quantified in business terms (revenue impact, customer trust, regulatory fines, operational disruption)
- **Dependencies**: Which assets depend on others; a compromise of a central dependency cascades
- **Ownership**: Who is accountable for protecting each asset? (data owner, system owner, compliance officer)

## Instructions

1. **Enumerate All Assets**: Inventory by category:
   - **Data Assets**: Customer PII, payment card data, trade secrets, API credentials, configuration files, logs, backups
   - **System Assets**: Web applications, APIs, backend services, admin dashboards, databases, caches, message queues
   - **Infrastructure Assets**: Cloud resources (VPCs, databases, storage), on-prem servers, load balancers, firewalls, DNS, certificates
   - **Credentials/Secrets**: API keys, OAuth tokens, database passwords, SSH keys, TLS certificates
   - **Personnel Assets**: Security-critical staff (admins, database owners, compliance officers), points of single failure

2. **Classify Each Asset**:
   - **Data Classification**: Public, Internal, Confidential, Restricted (based on sensitivity and regulatory requirements)
   - **Business Criticality**: Critical (business stops without it), High (significant disruption), Medium (degraded service), Low (nice to have)
   - **Recovery Requirements**: RTO (Recovery Time Objective), RPO (Recovery Point Objective)

3. **Document Dependencies**:
   - Does Asset B depend on Asset A? (e.g., API depends on database, application depends on external service)
   - What assets would compromise if central asset is breached? (e.g., if admin account is compromised, all systems are at risk)
   - Single points of failure? (e.g., one database server, one admin, one encryption key)

4. **Assign Financial Value** (if possible):
   - Direct value: Asset's revenue, cost of replacement
   - Indirect value: Business disruption, customer churn, regulatory fines, reputation damage
   - Use this to prioritize security investment

5. **Map to Controls**: Which assets require which protections? (encryption, access controls, backups, monitoring)

## Anti-Patterns

- Inventory that lists systems without valuing data; **data is the most critical asset; systems are just the means to protect/process it**
- Forgetting shadow IT and undocumented systems; **get engineering and operations to list systems they depend on; many are unknown to security**
- Treating all assets equally in risk assessment; **a compromised admin credential is worth vastly more than a compromised low-privilege account**
- Omitting soft assets like reputation, customer trust, or institutional knowledge; **these are valuable but harder to quantify**
- Treating asset inventory as a one-time effort; **update it quarterly as new services are deployed, old systems decommissioned, and dependencies change**

## Further Reading

- NIST SP 800-30 (Risk Assessment): Asset valuation and criticality determination
- ISO/IEC 27001:2022 (Information Security Management System): Asset identification and classification
- SANS Critical Security Controls: Asset Management (Control 1)
- Business Continuity Institute (BCI) Good Practice Guidelines: Asset identification for disaster recovery
