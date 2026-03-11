# Infrastructure Security Plugin

Cloud and infrastructure security toolkit covering cloud posture, network segmentation, container security, Kubernetes hardening, IAM, and zero-trust architecture.

## Skills

### 1. cloud-security-posture

Assess cloud infrastructure security using cloud-specific security controls (AWS Security Hub, Azure Security Center, GCP Security Health Analytics).

### 2. network-segmentation

Design network segmentation strategies (VPCs, subnets, security groups, NACLs) to isolate workloads and limit lateral movement.

### 3. container-security-review

Audit container images and runtime security (image scanning, runtime monitoring, seccomp, AppArmor).

### 4. kubernetes-security

Harden Kubernetes clusters through RBAC, network policies, pod security policies, and audit logging.

### 5. iam-policy-design

Design least-privilege IAM policies and role assumptions for cloud resources and services.

### 6. infrastructure-hardening

Harden servers and infrastructure through patching, OS configuration, and attack surface reduction.

### 7. certificate-management

Manage TLS certificates, CSRs, and automated renewal for infrastructure and applications.

### 8. zero-trust-architecture

Design zero-trust security models requiring verification at every access point, not perimeter defense.

## Commands

### audit-cloud

Assess cloud infrastructure security posture against cloud-specific controls and best practices.

### harden-infrastructure

Implement infrastructure hardening recommendations including OS patching, configuration, and segmentation.

### review-iam

Audit IAM policies and roles for least-privilege design and excessive permissions.

## Quick Start

1. **Cloud security assessment**: Use `audit-cloud` to assess cloud posture
2. **Infrastructure hardening**: Use `harden-infrastructure` to implement security controls
3. **IAM audit**: Use `review-iam` to audit identity and access management

## Plugin Info

- **Version**: 1.0.0
- **Author**: Seth Ford
- **License**: MIT
- **Keywords**: cloud, infrastructure, kubernetes, iam, zero-trust
