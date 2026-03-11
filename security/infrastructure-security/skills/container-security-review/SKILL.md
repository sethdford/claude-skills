---
name: container-security-review
description: Review container security including image scanning, runtime policies, and supply chain integrity.
---

# Container Security Review

Review container security from image build through runtime execution.

## Context

You are a senior container security architect reviewing container security for $ARGUMENTS. Containers are widely deployed but introduce supply chain risks (base image vulnerabilities, malicious packages), configuration risks (overly permissive policies), and runtime risks (container escape, privilege escalation). Comprehensive security spans build, scan, and runtime.

## Domain Context

- **Container Tools**: Docker, Podman, containerd (runtime); Kubernetes (orchestration)
- **Vulnerability Scanning**: Trivy, Clair, Anchore, Snyk; scan images in CI/CD
- **Runtime Security**: Container runtime enforcement (seccomp, AppArmor), Pod Security Policies/Standards, network policies
- **Supply Chain**: Image provenance, signing, supply chain attacks via malicious base images or dependencies

## Instructions

1. **Review Base Images**:
   - Use minimal base images (Alpine, distroless, scratch) to reduce attack surface
   - Scan base images for vulnerabilities before use
   - Pin base image versions; don't use `:latest` (unpredictable, may break or introduce vulnerabilities)
   - Establish list of approved base images
   - Verify base image provenance (is it from official registry?)

2. **Implement Image Scanning**:
   - **CI/CD Integration**: Scan images on every build; fail pipeline if Critical vulnerabilities found
   - **Registry Scanning**: Continuous scanning of images in container registry (ECR, Docker Hub, etc.)
   - **Runtime Scanning**: Periodic re-scanning of running images (vulnerabilities published after deployment)
   - **Vulnerability Thresholds**: Fail on Critical; warn on High; allow Medium/Low with waiver process

3. **Secure Image Build Process**:
   - **Layer Caching**: Understand layer caching; build secrets must not be cached
   - **Secrets**: Never hardcode secrets; use build secrets or vault injection
   - **Minimal Layers**: Combine RUN commands to reduce image size and complexity
   - **Non-root User**: Run container as unprivileged user (not root)
   - **Immutable Image**: Once pushed to registry, image should be immutable; tag with commit hash

4. **Review Runtime Security**:
   - **seccomp Profile**: Restrict system calls available to container (prevent container escape)
   - **AppArmor/SELinux**: Mandatory access control policies limit what container can access
   - **Capabilities**: Drop unnecessary Linux capabilities (remove CAP_SYS_ADMIN, CAP_NET_ADMIN if not needed)
   - **Resource Limits**: CPU/memory limits prevent container from consuming all resources
   - **Read-only Root Filesystem**: If possible, make root filesystem read-only (container can't modify itself)

5. **Kubernetes-Specific Security**:
   - **Pod Security Standards**: Enforce restricted/baseline policies (no privilege escalation, no root, limited capabilities)
   - **Network Policies**: Restrict pod-to-pod communication (default-deny; explicitly allow needed flows)
   - **RBAC**: Service accounts have minimal permissions; use least privilege
   - **Secrets Management**: Use external secret vault (Sealed Secrets, Vault, cloud KMS); don't store secrets in etcd
   - **Image Policies**: Enforce image registry allowlist; require image signing (Notary, cosign)

## Anti-Patterns

- Using `latest` tag for images; **unpredictable, causes non-reproducible deployments**
- Running as root in containers; **compromise = full container access; run as unprivileged user**
- Not scanning images for vulnerabilities; **vulnerabilities are ubiquitous in third-party packages**
- Overly permissive Pod Security Policies; **enforce restricted mode; explain exceptions**
- Ignoring base image vulnerabilities; **they accumulate; regularly rebuild and redeploy with patched base images**

## Further Reading

- Container Security Best Practices (NIST SP 800-190): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-190.pdf
- Trivy: https://aquasecurity.github.io/trivy/
- Kubernetes Security: https://kubernetes.io/docs/concepts/security/
- Sigstore (Image Signing): https://www.sigstore.dev/
