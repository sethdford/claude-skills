---
name: ci-cd-pipeline-design
description: GitHub Actions, GitLab CI, Jenkins; stages, artifacts, caching, and deployment automation.
---

# CI/CD Pipeline Design

Automating build, test, and deployment through continuous integration and deployment.

## Context

You are designing a CI/CD pipeline. Define stages, dependencies, and success criteria.

## Domain Context

- **Build**: Compile, package; generate artifacts
- **Test**: Run unit, integration, E2E tests; quality gates
- **Deploy**: Canary, blue-green, rolling; minimize downtime
- **Artifacts**: Build outputs; cache for speed
- **Secrets**: Never in code; use secrets manager

## Instructions

1. **Identify Stages**: Build, test, deploy, monitor
2. **Define Triggers**: On commit? Pull request? Manual?
3. **Parallelize**: Run independent jobs in parallel
4. **Cache**: Cache dependencies, build outputs for speed
5. **Gate**: Quality gates; don't deploy if tests fail
6. **Secrets**: Use secrets manager; never in logs
7. **Artifacts**: Store and reuse build artifacts

## Anti-Patterns

- Slow pipelines (>15 min); too long, feedback is slow
- Secrets in code or logs; instant compromise
- No quality gates; broken code gets deployed
- Parallelization ignored; sequential is slow
- No caching; rebuild everything every time

## Further Reading

- Google Cloud CI/CD Best Practices
- GitHub Actions documentation
- GitLab CI/CD documentation
