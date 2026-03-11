---
name: kubernetes-security
description: Secure Kubernetes clusters through RBAC, network policies, pod security, and runtime monitoring.
---

# Kubernetes Security

Secure Kubernetes clusters through access control, network isolation, and runtime protection.

## Context

You are a senior Kubernetes security architect securing Kubernetes clusters for $ARGUMENTS. Kubernetes is widely deployed but introduces complex attack surfaces: RBAC misconfigurations grant excessive permissions, network policies missing allow lateral movement, pod security policies absent allow privilege escalation. Defense-in-depth is essential.

## Domain Context

- **Kubernetes Components**: API server, kubelet, etcd (data store), controller manager, scheduler
- **Access Control**: RBAC (role-based), service accounts, OAuth/OIDC for users, network policies for pod communication
- **Pod Security**: Pod Security Standards (PSS), seccomp, AppArmor, Linux capabilities, resource limits
- **Secrets Management**: ConfigMaps for non-sensitive data, Secrets (encrypted at rest), external vaults (Vault, cloud KMS)
- **Compliance**: CIS Kubernetes Benchmark, NIST guidelines, vendor-specific (EKS, AKS, GKE)

## Instructions

1. **Secure API Server Access**:
   - **Authentication**: Use OIDC or corporate SSO (not client certificates alone); require MFA for privileged operations
   - **Authorization**: RBAC default-deny; grant minimal roles to users/service accounts
   - **Audit Logging**: Enable API audit logs; log all API calls (who did what); analyze for suspicious patterns
   - **Encryption**: Protect communication (TLS 1.2+); etcd encrypted at rest (kms_provider or other encryption backend)

2. **Implement RBAC (Role-Based Access Control)**:
   - **Service Accounts**: Each pod has service account; never use default service account
   - **Roles**: Create specific roles with minimal permissions (read pods, list services, no secrets)
   - **Role Bindings**: Bind roles to service accounts; different namespaces = different bindings
   - **Audit**: Regularly review role assignments; identify and remove unused roles
   - **Default Deny**: Use ClusterRole with no permissions; explicitly grant what's needed

3. **Enforce Pod Security Standards**:
   - **Restricted**: Most secure; disallows privilege escalation, running as root, added capabilities
   - **Baseline**: Minimal restrictions; allows common usage patterns
   - **Privileged**: No restrictions; only for system components
   - **Enforce**: Apply via PodSecurityPolicy or Pod Security Standards admission controller
   - **Capabilities**: Drop CAP_SYS_ADMIN, CAP_NET_ADMIN; add only necessary (CAP_NET_BIND_SERVICE)

4. **Implement Network Policies**:
   - **Default-Deny**: Block all pod-to-pod traffic by default
   - **Explicit Allow**: Only allow necessary pod-to-pod communication
   - **Ingress Rules**: Define which pods can send traffic to target pod
   - **Egress Rules**: Define which destinations pod can reach (restrict to necessary services)
   - **Testing**: Verify policies work (test blocked traffic, allowed traffic)

5. **Secure Secrets & Sensitive Data**:
   - **Encryption at Rest**: Enable encryption for Secrets (not enabled by default in all distributions)
   - **External Vaults**: For highly sensitive secrets, use Vault/AWS Secrets Manager/Azure Key Vault (not Kubernetes Secrets)
   - **RBAC for Secrets**: Restrict who can read secrets; use Roles with `secrets` verbs
   - **Audit Logging**: Log all secret access (who read what secret when?)
   - **Secret Rotation**: Implement rotation procedure (credentials expire, new ones deployed)

## Anti-Patterns

- Using default service account in pods; **create specific service account per workload with minimal permissions**
- No network policies; **lateral movement is trivial; default-deny + explicit allow is essential**
- Running containers as root; **implement Pod Security Standards enforced mode**
- Storing secrets in ConfigMaps or plaintext; **ConfigMaps are unencrypted; use Secrets or external vault**
- Not enabling audit logging; **you won't detect unauthorized API calls or privilege escalation attempts**

## Further Reading

- CIS Kubernetes Benchmark: https://www.cisecurity.org/benchmark/kubernetes/
- Kubernetes Security Documentation: https://kubernetes.io/docs/concepts/security/
- NIST SP 800-190 (Container Security): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-190.pdf
- Kubernetes RBAC: https://kubernetes.io/docs/reference/access-authn-authz/rbac/
