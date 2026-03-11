---
name: infrastructure-as-code-patterns
description: Codify infrastructure with Terraform, CloudFormation, or Pulumi. Design IaC architecture, versioning, testing, and drift detection. Use when automating infrastructure or establishing IaC practices.
---

# Infrastructure-as-Code Patterns

Define and manage infrastructure through code for reproducibility, version control, and automation.

## Context

You are building infrastructure-as-code practices. Choose tools, design module structure, plan testing and validation, implement drift detection. Read current infrastructure, team programming skills, and cloud platform.

## Domain Context

Based on IaC best practices (Terraform, CloudFormation, Pulumi):

- **Declarative vs Imperative**: Declare desired state (Terraform) vs describe steps (CloudFormation). Declarative is more maintainable.
- **Modularity**: Reusable modules (VPC, database, load balancer); parameterized for different environments
- **State Management**: Terraform state tracks infrastructure; must be versioned and backed up
- **Testing**: Unit tests (validate syntax), integration tests (deploy to staging), policy tests (compliance)
- **Drift Detection**: Find manual changes not in code; reconcile or remediate

## Instructions

1. **Choose Tool**: Terraform (multi-cloud, popular, large ecosystem). CloudFormation (AWS-native, less learning). Pulumi (programming language, more flexible).

2. **Design Module Structure**: Root modules per environment (dev, staging, prod). Shared modules for common patterns (VPC, RDS cluster, service). Versioned modules in registry.

3. **Plan State Management**: Store state in remote backend (S3 + DynamoDB for Terraform). Enable versioning and locking. Restrict access (IAM for AWS state). Never commit state to Git.

4. **Implement Testing**: Validate syntax (terraform fmt). Unit tests (mock resources). Integration tests (deploy to ephemeral environment, test behavior). Destroy after test.

5. **Detect and Handle Drift**: Use `terraform plan` to detect changes not in code. Use policy as code (Sentinel, OPA) to enforce compliance. Periodically reconcile drift.

## Anti-Patterns

- **One Monolithic Module**: All infrastructure in single file. Result: hard to understand, reuse, test. **Guard**: Break into modules; each module responsible for logical unit.
- **State Committed to Git**: Store state in version control. Result: leaks credentials, creates merge conflicts. **Guard**: Remote state backend; ignore .tfstate in Git.
- **No Testing**: Deploy to production first time. Result: broken infrastructure. **Guard**: Test in ephemeral environment; validate before production.
- **Ignoring State Locking**: Multiple people apply changes simultaneously. Result: state corruption. **Guard**: Use remote backend with locking; enforce plan review before apply.

## Further Reading

- _Terraform: Up and Running_ by Yevgeniy Brikman — foundational IaC patterns
- _Infrastructure as Code_ by Kief Morris — IaC principles and practices
- _Pulumi Documentation_ — multi-language IaC approach
