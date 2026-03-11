---
description: Assess cloud infrastructure security posture against cloud-specific controls and best practices.
argument-hint: [cloud provider: aws/azure/gcp, account id or subscription id]
---

# Audit Cloud Command

Chain these steps:

1. Use `cloud-security-posture` to assess cloud infrastructure using native security tools
2. Use `network-segmentation` to verify network isolation and security group rules
3. Use `container-security-review` to audit container images and runtime
4. Use `iam-policy-design` to review IAM policies for least privilege

Deliverables:

- Cloud security posture assessment with scores
- Network segmentation review
- Container security findings
- IAM policy recommendations

After completion, suggest follow-up commands: `harden-infrastructure`, `review-iam`.
