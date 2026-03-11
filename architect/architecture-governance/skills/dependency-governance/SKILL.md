---
name: dependency-governance
description: Manage and optimize system dependencies (libraries, services, data). Reduce coupling, track vulnerabilities, plan deprecation. Use when managing dependency sprawl or improving system modularity.
---

# Dependency Governance

Systematically manage dependencies to reduce coupling, track vulnerabilities, and maintain security.

## Context

You are governing dependencies in the system. Reduce external library reliance, manage service dependencies, deprecate old systems. Read dependency graphs, vulnerability reports, deployment constraints.

## Domain Context

Based on dependency management and architectural modularity:

- **Library Dependencies**: Third-party code you compile into application. Vulnerability risk, maintenance burden, version conflicts.
- **Service Dependencies**: Other services your system calls (REST, gRPC, message queues). Coupling, availability risk, latency impact.
- **Data Dependencies**: Databases, caches, data lakes shared between systems. Schema coupling, migration complexity.
- **Transitive Dependencies**: Dependencies of your dependencies. Hard to track, security risk. Dependency hell.

## Instructions

1. **Map Dependency Graph**: What does your system depend on? List direct dependencies (libraries, services, databases). Then transitive (dependencies of dependencies).

2. **Audit for Risk**: Libraries: any known vulnerabilities? Check with OWASP, CVE databases. Services: what's the SLA? What happens if it fails? Data: can you evolve schema independently?

3. **Reduce Coupling**: Remove unused libraries. Extract service dependencies into adapters (easier to swap). Copy small utilities instead of depending on library. Use event-driven instead of direct service calls.

4. **Version Management**: Update regularly; don't skip versions (harder to jump 5 versions than 1). Automate dependency updates (dependabot, renovate). Test each update in CI before merging.

5. **Plan Deprecation**: For dependencies you want to remove, announce timeline. Give teams 6-12 months to migrate. Finally remove or mark as deprecated. Track adoption.

## Anti-Patterns

- **Transitive Dependency Hell**: 100 libraries installed, only use 5. Result: bloated, security risk, slow builds. **Guard**: Audit transitive deps; remove heavy frameworks for simple use cases.
- **Version Pinning Forever**: Pin to old version to avoid updates. Result: security vulnerabilities, incompatibility with new tools. **Guard**: Regular updates; automate testing.
- **Service Coupling Without Fallback**: Service A calls Service B without retry logic. Result: cascading failure. **Guard**: Circuit breaker, fallback, timeout; design for fault tolerance.
- **No Deprecation Path**: Remove dependency without warning. Result: broken builds. **Guard**: Announce 6+ months early; provide migration guide; track adoption.

## Further Reading

- _Working with Legacy Code_ by Michael Feathers — managing large dependency bases
- _Release It!_ by Michael Nygard — designing for service dependency failures
- _Scaling Microservices_ by Sam Newman — dependency patterns in distributed systems
