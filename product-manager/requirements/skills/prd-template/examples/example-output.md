# Product Requirements Document: Quick Share Links

## Executive Summary

Freelance users struggle to share project progress with clients due to a complex permissions-based invitation flow, resulting in 67% abandonment and only 8% trial-to-paid conversion. This PRD specifies a simplified "Quick Share" feature that generates a one-click read-only shareable link, based on user testing showing this mental model is preferred. We expect this to improve trial-to-paid conversion to 25% for freelancers (+$180K annual ARR) and reduce support load by 4 hours/week.

---

## Problem Statement

**Link**: [Link to problem statement: "Retention Churn in Freelancer Onboarding"]

Freelancers want to share project visibility with clients but find the current permissions-based invitation flow too complex. Session recordings show 67% of freelancers abandon the invitation midway; support receives 12+ tickets/month from users confused by the permissions model. This PRD replaces the complex form-based flow with a one-click "Quick Share" link generation that mirrors familiar mental models (Dropbox, Google Drive).

---

## Success Metrics

| Metric                                             | Current   | Target     | Timeframe |
| -------------------------------------------------- | --------- | ---------- | --------- |
| Trial-to-paid conversion (freelancer segment)      | 8%        | 25%        | Q2 2024   |
| % of freelancers who share with a client by day 14 | 25%       | 50%        | Q2 2024   |
| Time to generate first share link                  | 8 min avg | <2 min avg | Q2 2024   |
| Support tickets re: sharing/permissions            | 12/month  | <3/month   | Q2 2024   |
| Return frequency for sharers vs. non-sharers       | 1x        | 4.2x       | Q2 2024   |

---

## User Stories

- As a freelance designer, I want to generate a share link with one click so that I can share project progress with my client without explaining permissions
- As a freelancer, I want the link to expire automatically after 30 days so that access is revoked automatically when the project ends
- As a team lead managing freelancers, I want to see all active shared links in my project settings so that I can manage who has access
- As a client viewing a shared project, I want to see project files and status updates without creating an account so that I can quickly understand what's been completed

---

## Functional Requirements

### Feature 1: Quick Share Link Generation

1. Users can generate a shareable link from the project detail view with one click ("Share" button in top toolbar)
2. Clicking "Share" immediately generates a URL-safe, cryptographically secure token (≥32 bytes entropy)
3. Generated link is displayed in a copy-to-clipboard interaction (button label: "Copy Link"; success feedback: toast notification "Link copied!")
4. Sharing a project for the first time triggers an informational modal explaining what the recipient can see (read-only access to files, timeline, comments)
5. Users can customize the share before generating the link: expiration date (default 30 days), permissions toggle (files only vs. files + comments)

### Feature 2: Shared Link Access Control

1. Shared link recipients gain read-only access to project files, timeline, and comments (configurable)
2. Shared link recipients cannot edit, delete, move, or upload files
3. Shared link recipients cannot add or remove collaborators
4. Shared link recipients can optionally add comments (configurable by link creator)
5. Shared link does not require recipient to have an account or password

### Feature 3: Link Management

1. Users can view all active shared links in project settings (link preview with expiration date, permissions, created date)
2. Users can revoke link access immediately from the management interface
3. Users can edit link settings (expiration date, permissions) without regenerating the link
4. Users can see who has accessed the link (if analytics are enabled in account settings)
5. Deleting a project automatically revokes all shared links; user receives notification

### Feature 4: Link Expiration & Security

1. Links expire after the specified expiration date (default 30 days; user-customizable to 1-365 days)
2. Accessing an expired link returns HTTP 403 with message "This link has expired" and CTA to request access from link creator
3. Revoking a link immediately returns HTTP 403 for any subsequent access
4. Link tokens use URL-safe encoding (no special characters that break email clients)
5. Link preview works in email clients without JavaScript (text content, no interactive elements)

---

## Non-Functional Requirements

- **Performance**: Link generation completes in <200ms (p99); shared link page load <1s on 3G (measured from first byte)
- **Accessibility**: Shared link page meets WCAG 2.1 AA standards (tested with axe DevTools); keyboard navigation fully functional
- **Security**:
  - Link tokens use cryptographically secure random generation (not sequential or predictable)
  - No PII in URL or page source
  - Link preview page does not set authentication cookies
  - HTTPS-only; no downgrade attacks
- **Scalability**: System supports 1M concurrent shared links per region; can handle 100 req/sec for shared link generation
- **Localization**: Shared link pages support 8 languages (English, Spanish, French, German, Portuguese, Italian, Dutch, Japanese); auto-detect from browser language

---

## Edge Cases & Boundary Conditions

| Edge Case                                        | Expected Behavior                                                                                                                                  |
| ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Shared project is deleted**                    | Shared link returns HTTP 404 with message "This project is no longer available"; user is offered option to request access from the project creator |
| **Shared project is made private**               | All existing shared links are immediately revoked; link creator is notified via email                                                              |
| **Link creator leaves the workspace**            | Active shared links remain accessible (ownership transfers to workspace); links are not revoked                                                    |
| **Recipient tries to download files**            | Read-only constraint prevents download; user sees message "Download not available for shared projects"                                             |
| **Link accessed from incognito/private mode**    | Works normally; no session storage; each page load treats visitor as new                                                                           |
| **User has no active projects**                  | "Share" button is disabled; tooltip explains "Create a project first to generate a share link"                                                     |
| **Link is shared in a forum/Slack**              | Anyone with the link can access (as intended); no rate limiting (to avoid breaking legitimate access patterns)                                     |
| **Shared link accessed >30 days after creation** | Returns 403 "Link has expired"; user can request access via email link                                                                             |
| **Recipient's IP is on a blocklist**             | Access is blocked; returns 403 "Access denied" (standard security response)                                                                        |
| **Project has 0 files**                          | Link still generates and works; recipient sees empty project message "No files yet"                                                                |

---

## Constraints & Assumptions

### Technical Constraints

- Must use existing Postgres database (no new infrastructure)
- Shared link pages must work without authentication (no sign-up friction for recipients)
- Link tokens must be URL-safe (no special characters that break email clients or get URL-encoded)
- Cannot use database auto-increment IDs for tokens (sequential patterns are a security risk)
- Must use OAuth 2.0 for API authentication; do not implement custom auth for this feature

### Business Constraints

- Feature must ship by end of Q2 2024 (sales deadline for freelancer market messaging)
- Shared links are available on all plans (including free tier) to maximize adoption
- No additional server costs allowable; must run within existing infrastructure budget
- Support team must be trained and ready by launch date (2-hour training session required)

### Assumptions

- We assume freelancers prefer read-only sharing by default (based on user testing; n=12 users)
- We assume most shares last <30 days (based on usage data from competitors; median project lifecycle ~3 weeks)
- We assume recipients don't need to see edit history or version control (out of scope for MVP)
- We assume Enterprise customers will want SSO integration and audit logs; not in scope for MVP

---

## Design Specifications

### Key Screens/Flows

**Screen 1: Project Detail View (Share Button)**

- "Share" button added to top toolbar (right side, next to "More options")
- Button shows link icon; label: "Share"
- Clicking opens share modal

**Screen 2: Quick Share Modal**

- Heading: "Share Project"
- Informational text: "Anyone with this link can view your project (read-only)"
- Generated link displayed in text field (copy-to-clipboard button on right)
- Settings section (collapsible):
  - "Link expires in": dropdown (1 day, 7 days, 30 days, 90 days, 1 year, or custom date picker)
  - "Recipients can": checkbox (Files only / Files + Comments)
- "Generate new link" button (regenerates link if user wants fresh token)
- Close button or backdrop click to dismiss

**Screen 3: Project Settings → Share Tab**

- Heading: "Active Share Links"
- Table: Created | Expires | Permissions | Actions
- Each row shows: creation date, expiration date, permission level (Files only / Files + Comments), action buttons (Edit, Revoke, Copy)
- "Generate new link" button at bottom
- Message if no active links: "No active share links"

**Screen 4: Shared Project Recipient View**

- Header: Project name + "Shared by [creator name]"
- File browser (read-only mode; no edit/delete/upload buttons)
- Timeline showing project updates
- Comments section (view only if permissions allow)
- Footer: "This is a shared project. You don't need an account to view this."

### Information Architecture

- Shared links are project-level (not file-level); simplifies permission model for MVP
- All shared links for a single project use the same access rule (either all files-only, or all files+comments)
- Link management lives in Project Settings (not in main toolbar) to avoid cluttering UI
- Recipient viewing shared project has no access to settings or admin controls

### Design Links

- Wireframes: [Figma link: Quick Share Feature]
- Prototypes: [Interactive prototype for user testing]

---

## Acceptance Criteria

- [ ] User can generate a share link from project detail view in one click
- [ ] Link generation completes in <200ms (monitored via performance APM)
- [ ] Generated link is URL-safe; works in email clients without encoding issues
- [ ] Copy-to-clipboard interaction works on desktop and mobile
- [ ] Shared link recipient can view files without login
- [ ] Shared link recipient cannot edit, delete, or upload files (read-only enforced by API)
- [ ] Shared link recipient can optionally add comments (if enabled by creator)
- [ ] Link expires after specified expiration date; accessing expired link returns 403
- [ ] User can revoke link; revoked link immediately returns 403
- [ ] User can edit link settings (expiration, permissions) without regenerating link
- [ ] Project deletion automatically revokes all shared links
- [ ] Shared link page is responsive and readable on mobile (tested at 320px, 768px, 1200px widths)
- [ ] Shared link page meets WCAG 2.1 AA accessibility standards (axe DevTools audit passes)
- [ ] No PII is exposed in URL or page source code
- [ ] Link tokens use ≥32 bytes cryptographic entropy (verified via code review)
- [ ] Shared link generation scales to 100 req/sec without degradation (load tested)
- [ ] Support team can answer "How do I share a project?" in <2 minutes

---

## Out of Scope

- **Edit-access sharing**: Recipients can only view (read-only). Write-access sharing is a future enhancement.
- **File-level sharing**: Links grant access to entire project. Granular file-level permissions are out of scope for MVP.
- **Persistent links**: Links expire after configurable period. Permanent share links are not supported.
- **SSO/SAML integration**: Shared links work via URL only. Enterprise SSO is out of scope for MVP.
- **Audit logs**: We don't track who viewed a shared link (analytics are optional, configurable per account).
- **Password-protected links**: Links are URL-only access. Password protection is a future enhancement.
- **Watermarking**: Shared files are not watermarked. Watermarking is out of scope.

---

## Dependencies & Integrations

### Internal Dependencies

- **Backend team**: Implement token generation, expiration, permission enforcement; link revocation API
- **Frontend team**: Implement share modal, project settings share tab, shared recipient view
- **QA team**: Verify all acceptance criteria; test on multiple browsers; performance testing
- **Support team**: Training on sharing feature; prepare FAQ and support docs; monitor support ticket volume

### External Integrations

- **Email service** (existing): Send notification when project creator wants to share
- **Analytics** (optional): Track shared link access patterns (opt-in per account)

---

## Timeline & Phases

| Phase         | Duration                  | Deliverables                                                                      |
| ------------- | ------------------------- | --------------------------------------------------------------------------------- |
| Design Review | 1 week (Feb 12-16)        | Approved wireframes, design spec, accessibility review                            |
| Engineering   | 3 weeks (Feb 19 - Mar 11) | Backend API complete, frontend complete, internal QA pass                         |
| QA & Testing  | 1 week (Mar 12-18)        | All acceptance criteria verified, load testing passed, accessibility audit passed |
| Launch        | Mar 19                    | Feature live in production; support trained                                       |

---

## Success Definition

**Shipping criteria** (all must be true to ship):

- [ ] All acceptance criteria passed by QA
- [ ] No critical bugs; <3 P2 bugs remaining
- [ ] Design review approved by design lead
- [ ] Engineering review approved by tech lead
- [ ] Performance benchmarks met (<200ms link generation, <1s page load)
- [ ] Security review passed (token entropy, no PII exposure)
- [ ] Monitoring/alerts configured (broken links, error rates, page performance)
- [ ] User documentation complete (help center article, in-app tooltips)
- [ ] Support team trained and ready

**Post-launch success criteria** (measure after 2 weeks, March 26):

- Trial-to-paid conversion for freelancers trending toward 20%+ (from 8% baseline)
- <4 support tickets/week related to sharing (from 12/week baseline)
- Shared link page load time <1s on 3G (monitoring confirms)
- No critical production issues or security incidents

---

## Metrics Dashboard

[Link to Looker dashboard: Quick Share Feature KPIs]

- Trial-to-paid conversion by segment
- Daily active sharers
- Support ticket volume
- Page load performance metrics
- Error rate monitoring

---

## Document Metadata

| Property     | Value                                                      |
| ------------ | ---------------------------------------------------------- |
| Status       | Ready for Design Review                                    |
| Owner        | Sarah Chen, Product Manager                                |
| Last Updated | 2024-02-12                                                 |
| Created      | 2024-02-10                                                 |
| Stakeholders | Product, Design, Backend, Frontend, QA, Support, Analytics |
