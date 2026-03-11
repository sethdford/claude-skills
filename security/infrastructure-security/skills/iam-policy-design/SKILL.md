---
name: iam-policy-design
description: Design and implement least-privilege IAM policies for cloud and on-premise environments.
---

# IAM Policy Design

Design and implement least-privilege Identity and Access Management (IAM) policies.

## Context

You are a senior IAM architect designing policies for $ARGUMENTS. IAM is the foundation of access control; overly permissive policies enable privilege escalation and lateral movement. Well-designed IAM follows least-privilege: each identity (user, service account) has only the permissions needed for their job.

## Domain Context

- **IAM Concepts**: Identity (users, service accounts, roles), Resource (servers, databases, S3 buckets), Action (read, write, delete), Policy (rules defining what actions are allowed)
- **Cloud IAM**: AWS IAM (users, roles, policies), Azure RBAC (role assignments), Google Cloud IAM (predefined roles, custom roles)
- **On-Premise IAM**: Active Directory (users, groups), LDAP, privilege management tools (Delinea, Okta)
- **Privilege Escalation**: Paths from low-privilege identity to admin; mitigation: least privilege + monitoring

## Instructions

1. **Define Identity Categories**:
   - **Human Users**: Developers, DevOps, security engineers, contractors (varying permission levels)
   - **Service Accounts**: Applications, CI/CD pipelines, managed identities (minimal permissions for function)
   - **Administrative Roles**: Admins, on-call engineers (elevated permissions, auditable)
   - **Third-Party**: Vendors, contractors, external integrations (temporary, scoped access)

2. **Implement Least-Privilege Access**:
   - **Principle of Least Privilege**: Each identity has minimum permissions needed for role
   - **Role-Based Access Control (RBAC)**: Assign pre-defined roles (Developer, Admin, Viewer); don't grant individual permissions
   - **Resource-Based Policies**: Grant access to specific resources, not wildcards
   - **Conditions**: Time-based access (developer access 9-5), IP-based (corporate network only), MFA-required
   - **Regular Review**: Quarterly audit of permissions; remove unused, add necessary, fix over-privileges

3. **Design Cloud IAM Policies**:
   - **AWS IAM**:
     - Use managed policies (AWS-provided, well-tested) as base
     - Create custom policies for organization-specific access
     - Use Roles for temporary, assumable access (EC2 instance role, cross-account role)
     - Avoid IAM users; prefer federated access (SAML, OIDC)
   - **Azure RBAC**:
     - Use built-in roles (Contributor, Reader, Viewer)
     - Create custom roles for specific workloads
     - Use managed identities for Azure services
   - **Google Cloud IAM**:
     - Predefined roles cover most use cases
     - Custom roles for specific needs
     - Service accounts for applications

4. **Manage Service Account Permissions**:
   - **Least Privilege**: Each service account has only permissions it needs
   - **Separate Accounts**: Different accounts for different purposes (CI/CD, production, development)
   - **Time-Limited Credentials**: Use short-lived tokens (JWT, short-term AWS keys) instead of long-term keys
   - **Audit Trail**: All service account actions logged (CloudTrail, audit logs)
   - **Rotation**: Regularly rotate credentials; revoke old ones

5. **Monitor & Audit IAM**:
   - **Access Reviews**: Quarterly review of who has what permissions
   - **Anomaly Detection**: Alert on unusual access patterns (user accessing new resources, access outside work hours)
   - **Logging**: Ensure all IAM changes are logged and immutable (CloudTrail, Azure Activity Log)
   - **Reporting**: Generate IAM compliance reports (who has admin, who has database access, etc.)

## Anti-Patterns

- Using wildcard permissions (`"Action": "*"`, `"Resource": "*"`); **specify exact actions and resources**
- Creating super-admin roles for developers; **use least privilege; escalate on-demand**
- Not rotating service account credentials; **old compromised keys remain valid**
- Granting permissions to groups that are too broad; **create specific groups per job function**
- No logging of IAM changes; **you won't detect unauthorized access grants or privilege escalation**

## Further Reading

- AWS IAM Best Practices: https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
- Azure RBAC: https://docs.microsoft.com/en-us/azure/role-based-access-control/
- Google Cloud IAM: https://cloud.google.com/iam/docs
- NIST SP 800-53 (Access Control): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf
