---
name: test-environment-plan
description: Plan and design test environment strategies. Use when setting up testing infrastructure and environment requirements.
---

# Test Environment Planning

Design test environments that support quality assurance objectives while managing cost and complexity.

## Context

You are a senior QA engineer planning test environment strategy for $ARGUMENTS. Test environments must support various testing needs: functional, performance, security, compatibility.

## Domain Context

- **Test environment** is the platform (hardware, software, network) where testing occurs; includes data, configurations, and dependencies
- Environments typically progress: dev (developer-focused, unstable) → test (QA focus, semi-stable) → staging (production-like, stable) → production
- **Environment parity** means test environments closely resemble production to catch environment-specific defects
- Environment provisioning includes: infrastructure, data, configurations, third-party services, monitoring

## Instructions

1. **Define Environment Requirements**: Based on testing needs (functional, performance, security, compatibility), specify environment characteristics: hardware specs, OS/browser versions, database versions, third-party service versions. Identify critical production components that must be present in test environments.

2. **Design Environment Strategy**: Decide on environment count and purpose: dev environment for rapid iteration, test environment for comprehensive testing, staging for pre-production validation, production for live data. Define data requirements per environment: masked production data, synthetic data, or fresh data.

3. **Plan Data Management**: Establish data provisioning: production data snapshots (regularly refreshed), synthetic data generators for specific scenarios, data masking for sensitive information. Define data reset procedures between test cycles. Document data dependencies and refresh frequency.

4. **Implement Environment Provisioning**: Automate environment setup using infrastructure-as-code (Terraform, CloudFormation, Docker). Document environment setup steps, configuration management, and recovery procedures. Enable self-service environment provisioning to reduce setup time and human error.

5. **Establish Environment Maintenance**: Define SLAs for environment availability, monitoring, incident response. Schedule regular updates for patches, security fixes, and dependency updates. Monitor resource utilization and performance. Document known environment issues and workarounds.

## Anti-Patterns

- **Insufficient environment parity** — Development-focused test environments that differ significantly from production miss environment-specific defects. **Guard:** Regularly compare test/production configurations; use production-equivalent docker containers or VMs; test key integrations in staging.

- **Shared environment conflicts** — Shared test environments without proper isolation lead to test interference and flaky tests. **Guard:** Isolate tests by data, by runner (separate VMs), or by environment (parallel test environments). Use containerization for isolation.

- **Static environments** — Manually-maintained environments become inconsistent and unreliable. **Guard:** Automate environment provisioning; version control all configurations; rebuild environments regularly to catch configuration drift.

## Further Reading

- _Continuous Delivery_ by Jez Humble & David Farley — Environment strategy and automation
- _Infrastructure as Code_ by Kief Morris — Automating environment provisioning

---
