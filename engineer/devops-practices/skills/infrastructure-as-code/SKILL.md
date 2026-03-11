---
name: infrastructure-as-code
description: Terraform, CloudFormation, reproducible infrastructure, version control, and IaC best practices.
---

# Infrastructure as Code

Managing infrastructure through code; version controlled, auditable, reproducible.

## Context

You are writing infrastructure as code. Treat it like software; test, review, version.

## Domain Context

- **Declarative**: Describe desired state; tool figures out changes
- **Version Control**: Infrastructure changes tracked like code
- **Review**: Infrastructure changes go through pull requests
- **Reproducible**: Same code → same infrastructure
- **Idempotent**: Running twice is same as running once

## Instructions

1. **Use IaC**: Terraform, CloudFormation, Pulumi; pick one
2. **Version Control**: Commit infrastructure code
3. **Code Review**: Pull requests for all changes
4. **Modules**: Reusable components; DRY principle
5. **Secrets**: Never commit secrets; use secrets manager
6. **State**: Manage state file carefully; backup, lock
7. **Testing**: Test infrastructure like code

## Anti-Patterns

- Manual changes outside IaC; infrastructure drifts
- Secrets in code; instant compromise
- Massive monolithic infrastructure files; hard to review
- No version control; can't audit changes, can't rollback
- Testing infrastructure only in prod; catch errors early

## Further Reading

- Terraform documentation
- AWS CloudFormation best practices
- IaC best practices (O'Reilly)
