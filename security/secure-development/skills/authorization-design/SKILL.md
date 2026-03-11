---
name: authorization-design
description: Design authorization systems (access control, role-based permissions, principle of least privilege) to enforce fine-grained access policies.
---

# Authorization Design

Design fine-grained authorization systems using least privilege and role-based or capability-based access control.

## Context

You are a senior security architect designing authorization for $ARGUMENTS. Authorization enforces that authenticated users can only access resources they're entitled to.

## Domain Context

- **Principle of Least Privilege**: Grant minimum necessary permissions; default deny, explicit allow
- **Role-Based Access Control (RBAC)**: Users assigned roles (Admin, Editor, Viewer); roles have permissions
- **Attribute-Based Access Control (ABAC)**: Permissions based on attributes (user department, resource owner, time of day)
- **Capability-Based Access Control**: Users hold unforgeable tokens granting access; more fine-grained than RBAC

## Instructions

1. **Design Roles & Permissions**:
   - Identify roles (Admin, Moderator, User, Guest)
   - Define permissions for each resource/action (Read, Write, Delete, Admin)
   - Assign roles to users; never grant permissions directly
   - Example:
     ```
     Admin: Read/Write/Delete all resources
     Moderator: Read all; Write/Delete own posts and user-reported content
     User: Read all; Write own content; Delete own content
     Guest: Read public content only
     ```

2. **Implement Least Privilege**:
   - Default deny; explicitly grant permissions
   - Users get minimum necessary role; not Admin by default
   - Service accounts: create per-service accounts with narrow permissions (not shared root account)
   - Time-bound permissions: grant temporary elevated access for specific tasks, then revoke

3. **Enforce Authorization Checks**:
   - Check authorization on **every action**, not just page load
   - Check on API endpoints; never trust client-side authorization
   - Verify user owns resource before allowing delete: `if (post.owner_id != current_user.id) { deny }`
   - Check both object ownership and global permissions (user might be forbidden from resource)

4. **Prevent Common Authorization Bypasses**:
   - Insecure Direct Object Reference (IDOR): Verify user owns `/posts/{post_id}` before returning
   - Parameter Tampering: Don't trust client-provided role or permission parameters
   - Vertical Escalation: Don't assume "user" role can't access "admin" pages; enforce on every page
   - Horizontal Escalation: Verify user can only access own resources (own profile, own posts)

5. **Audit Authorization Decisions**:
   - Log permission denials (possible reconnaissance or attack)
   - Alert on privilege escalation attempts
   - Regular review of role assignments (who has admin access?)

## Anti-Patterns

- Hard-coding authorization in UI (hiding admin button from users); **client-side authorization is not authorization; always check server-side**
- Checking authorization only on page load; **check on every action; a token might become invalid mid-session**
- Allowing "root" or "admin" accounts for service-to-service communication; **create service accounts with minimal necessary permissions**
- Permanently assigning high-privilege roles; **use temporary elevation with time limits and audit trails**
- Trusting role names from JWT/API response; **always verify against backend permission store; JWT can be forged if signing key is compromised**

## Further Reading

- OWASP Authorization Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html
- CWE-639: Authorization Bypass through User-Controlled Key
- NIST SP 800-63C (Federation and Assertions): Role mapping and authorization in federated systems
