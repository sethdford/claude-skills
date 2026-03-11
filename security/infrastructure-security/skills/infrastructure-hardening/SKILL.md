---
name: infrastructure-hardening
description: Harden infrastructure through patch management, service hardening, and secure baselines.
---

# Infrastructure Hardening

Harden infrastructure through patch management, service configuration, and security baselines.

## Context

You are a senior infrastructure security engineer hardening systems for $ARGUMENTS. Hardening reduces attack surface by disabling unnecessary services, applying patches, securing configurations, and enforcing strong security baselines. Hardened systems are more resilient to attacks and easier to defend.

## Domain Context

- **CIS Benchmarks**: Industry-standard hardening guides (Linux, Windows, Docker, Kubernetes, cloud platforms)
- **Patch Management**: OS patches, application patches, firmware updates; critical for vulnerability remediation
- **Service Hardening**: Disable unnecessary services, remove unnecessary packages, secure remaining services
- **Compliance**: CIS Controls, NIST SP 800-53, PCI-DSS all require hardening
- **Baseline Images**: Pre-hardened OS images used for deployment (reduce manual effort)

## Instructions

1. **Select & Follow Hardening Baselines**:
   - **CIS Benchmarks**: https://www.cisecurity.org/cis-benchmarks/
     - Linux: Disable unnecessary services, enable SELinux/AppArmor, harden SSH, file permissions
     - Windows: Disable unnecessary services, enable Defender, restrict account policies, audit logging
     - Docker/Kubernetes: Pod security, network policies, RBAC (detailed in container-security-review, kubernetes-security)
   - **DISA STIGs**: https://public.cyber.mil/stigs/ (Government standards for hardening)
   - **Vendor Guidelines**: Follow OS and platform-specific hardening guidance

2. **Implement Patch Management**:
   - **Inventory**: Maintain inventory of all assets (servers, applications, firmware)
   - **Baseline**: Establish patching baseline (when patches are applied relative to release)
   - **Critical**: Apply critical patches within 24-48 hours (remotely exploitable vulnerabilities)
   - **High**: Apply within 1-2 weeks
   - **Medium/Low**: Apply within monthly/quarterly cycle
   - **Testing**: Test patches in staging before deploying to production
   - **Automation**: Use patch management tools (AWS Systems Manager, Azure Update Management, Puppet, Ansible)

3. **Harden Services**:
   - **SSH** (remote access):
     - Disable root login; disable password auth (use keys only)
     - Change default port (reduces noise); restrict to known IPs if possible
     - Enable logging; monitor for brute force
   - **Web Servers** (Apache, nginx):
     - Disable unnecessary modules; remove default pages
     - Configure TLS properly (1.2+, strong ciphers)
     - Restrict HTTP methods (e.g., disable TRACE)
   - **Databases**: Restrict network access, enable encryption, strong passwords, audit logging
   - **DNS**: Use DNS securely (DNSSEC), restrict zone transfers, configure firewall rules

4. **Disable Unnecessary Services & Packages**:
   - **Audit**: Identify running services; justify each one
   - **Remove**: Uninstall packages not needed for function
   - **Disable**: System services (telnet, Bluetooth, USB) should be disabled if not used
   - **Minimal Images**: Use minimal OS images (Alpine, distroless) to reduce surface area
   - **Regular Review**: Quarterly audit for service/package creep

5. **Implement Security Baselines & Automation**:
   - **Hardened Images**: Create baseline OS/container images with CIS hardening applied
   - **Infrastructure as Code**: Use Terraform, CloudFormation, Ansible to deploy hardened infrastructure consistently
   - **Compliance Scanning**: Automated scanning to verify baselines are maintained (AWS Config, Azure Policy, OpenSCAP)
   - **Continuous Remediation**: Auto-remediate simple violations (disable service, apply setting); alert on complex ones

## Anti-Patterns

- Manual hardening (prone to error); **use automation and baseline images**
- Infrequent patching; **vulnerabilities accumulate; patch regularly**
- Over-hardening (disabling legitimate functionality); **balance security and usability**
- Hardening without verification; **test hardened systems to ensure they function correctly**
- No baseline enforcement; **hardening reverts without continuous scanning and remediation**

## Further Reading

- CIS Benchmarks: https://www.cisecurity.org/cis-benchmarks/
- DISA STIGs: https://public.cyber.mil/stigs/
- NIST SP 800-53 (System Hardening): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf
- OpenSCAP (Hardening Compliance): https://www.open-scap.org/
