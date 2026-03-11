---
name: data-governance
description: Establish data ownership, quality standards, compliance policies, and metadata management. Build organizational data practices. Use when defining data strategy or improving data quality and compliance.
---

# Data Governance

Establish organizational data management practices, ownership, quality standards, and compliance policies.

## Context

You are building data governance practices. Define who owns data, how quality is enforced, compliance requirements, and metadata standards. Read organizational context, regulatory requirements, and existing data practices.

## Domain Context

Based on enterprise data management practices:

- **Data Ownership**: Clear accountability for data quality, availability, and compliance
- **Data Lineage**: Track data origin, transformations, and dependencies
- **Data Quality**: Accuracy, completeness, timeliness, consistency standards
- **Metadata Management**: Catalog of data assets, definitions, classifications
- **Compliance**: GDPR, CCPA, HIPAA, SOC2; data retention, access control
- **Master Data**: Golden record of critical entities (customer, product); source of truth

## Instructions

1. **Define Data Owner Roles**: Who is accountable for each data domain? Product for customer data, Finance for transaction data. Owners define quality standards and usage policies.

2. **Establish Metadata Catalog**: Inventory all data assets: databases, tables, APIs, data lakes. For each: owner, description, lineage (source), refresh frequency, classification (public/confidential/PII).

3. **Set Quality Standards**: For critical datasets, define SLAs: freshness (how recent), completeness (% non-null), accuracy (validated against source), consistency (matches across systems).

4. **Build Data Dictionary**: Business definitions of key entities and attributes. Customer means "active subscriber". Amount means "invoice total in USD". Shared vocabulary reduces confusion.

5. **Implement Access Control**: Who can access what data? Implement principle of least privilege. GDPR: individuals can request deletion; log access to sensitive data.

## Anti-Patterns

- **Governance Without Buy-In**: Impose rules without business input. Result: ignored policies. **Guard**: Make data owners responsible for enforcement; governance enables business not obstructs.
- **Metadata Without Updates**: Catalog created, then becomes stale. Result: inaccurate documentation. **Guard**: Automate metadata collection; make updates part of data pipeline changes.
- **No Enforcement Mechanism**: Quality standards defined but not checked. Result: bad data in pipelines. **Guard**: Implement automated data quality checks; fail on breach.
- **Treating Governance as IT-Only**: Business doesn't understand or support. Result: resistance, workarounds. **Guard**: Governance is business decision; IT implements and enforces.

## Further Reading

- _Data Governance_ by Donna Burbank and Katherine Giles — comprehensive governance framework
- _Fundamentals of Data Engineering_ by Joe Reis and Matt Housley — governance in practice
- _GDPR Compliance_ — regulatory context for privacy-centric governance
