---
name: test-data-strategy
description: Design test data management approaches. Use when planning data provisioning for testing.
---

# Test Data Strategy

Plan and execute test data provisioning that supports comprehensive testing while protecting sensitive information.

## Context

You are a senior QA engineer designing test data strategy for $ARGUMENTS. Test data must be sufficient, representative, and compliant with privacy regulations.

## Domain Context

- **Test data** includes all data inputs needed for testing: valid scenarios, edge cases, invalid inputs, boundary conditions
- **Data sources** include: production snapshots (masked), synthetic data, manual entry, API calls, database dumps
- **Data privacy** requires masking or anonymizing sensitive information (PII, financial data, health information)
- **Test data lifecycle** involves: provisioning (creation), masking (anonymization), refresh (updates), archival (cleanup)

## Instructions

1. **Analyze Data Requirements**: Map what data is needed for each test: functional tests (valid/invalid inputs, boundary cases), performance tests (realistic volumes), security tests (sensitive data scenarios). Identify data dimensions: range, volume, distribution, relationships. Document dependencies between data entities.

2. **Design Data Sources**: Decide on data provisioning approach: production snapshots (most realistic but privacy concerns), synthetic data (privacy-safe but may miss edge cases), hybrid (real structure, synthetic values). For each test type, specify which source is appropriate.

3. **Implement Data Masking**: If using production data, mask sensitive fields: replace names with synthetic names, anonymize phone/email, hash financial data. Ensure masked data remains realistic for testing (e.g., credit card format must be valid for validation tests).

4. **Automate Data Provisioning**: Use scripts to generate synthetic data, transform production data, or refresh test databases. Enable fast data reset between test cycles. Document data provisioning procedures and execution times. Make provisioning repeatable and version-controlled.

5. **Plan Data Lifecycle**: Define refresh frequency (daily, weekly, before major test cycles), retention periods (delete old test data), and compliance (GDPR deletion rights for masked production data). Monitor data quality: ensure synthetic data reflects real-world distributions, validate masked data for testing adequacy.

## Anti-Patterns

- **Using real sensitive data in test environments** — Exposes customer PII to unnecessary risk. **Guard:** Always mask production data before using in test environments; implement access controls; document compliance procedures.

- **Insufficient data variety** — Test data covering only happy paths misses edge cases and boundary bugs. **Guard:** Include invalid inputs, boundary values, large datasets, special characters, empty/null values in test data.

- **Manual data provisioning** — Slow, error-prone, difficult to reproduce. **Guard:** Automate data provisioning; use database snapshots, synthetic data generators, or API-based data creation; version control data generation scripts.

## Further Reading

- _Effective Software Testing_ by Effective Software Testing — Test data design strategies
- _GDPR and Test Data_ — Privacy compliance for test data management

---
