---
description: Audit IAM policies and roles for least-privilege design and excessive permissions.
argument-hint: [cloud provider or IAM policy list]
---

# Review IAM Command

Chain these steps:

1. Use `iam-policy-design` to audit current IAM policies and roles
2. Assess permission creep and identify overly permissive policies
3. Design least-privilege roles aligned with job functions

Deliverables:

- IAM audit report with policy assessment
- Permission creep analysis (users with excessive permissions)
- Least-privilege role design recommendations
- Remediation roadmap for policy simplification

After completion, suggest follow-up commands: `audit-cloud`, `harden-infrastructure`.
