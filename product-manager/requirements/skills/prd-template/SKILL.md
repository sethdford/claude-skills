---
name: prd-template
description: Create clear, unambiguous product requirements that prevent costly rework and enable execution. Use when scoping features, defining acceptance criteria, or ensuring alignment between product, design, and engineering.
allowed-tools: Read, Grep, Glob, Write, Edit
---

# PRD: Product Requirements Document

Create specifications that translate customer problems into executable requirements, complete with testable acceptance criteria and clear constraints.

## Context

You are a senior product manager writing a PRD to guide design and engineering execution. A well-written PRD prevents rework, reduces meeting overhead, and enables teams to move in parallel. Poor PRDs waste engineering time (building the wrong thing), create ambiguity during QA (what does "done" mean?), and make design reviews contentious (did we solve the problem?).

A PRD is not a design spec (that's design's job) or a technical architecture doc (that's engineering's job). A PRD is the contract between product, design, and engineering that defines _what_ we're building and _why_, leaving implementation details to the teams.

## Domain Context

- **Marty Cagan's "Inspired"**: PRDs serve as shared understanding between cross-functional teams; ambiguity in requirements translates to rework
- **"Acceptance Criteria" (agile)**: Testable definition of done—if acceptance criteria are vague ("responsive design"), the work isn't done until you define testability
- **Lean Startup principle**: Requirements should be validated against customer problem before engineering effort begins; a PRD without evidence of the underlying problem is speculation
- **Traceability**: Requirements should link back to the problem statement, forward to design specs and test plans
- **Edge cases**: The difference between a mediocre product and a polished one is handling of edge cases (empty state, error recovery, boundary conditions)
- **Constraints are requirements**: Technical, business, and timeline constraints are as important as feature requirements

## When to Use This Skill

- You've validated a customer problem and are ready to define a solution
- You're scoping a feature for multiple engineering teams and need a single source of truth
- Design and engineering are debating what "done" looks like; you need explicit acceptance criteria
- You're handing off work to another team or contractor; you need unambiguous specs
- You're planning a feature that touches multiple systems (payments, notifications, reporting); you need to define integration contracts

## Prerequisites

Before writing a PRD, gather:

1. **Problem statement**: What customer problem are we solving? (Link to problem discovery)
2. **Design direction**: Wireframes or prototypes showing the interaction model (not pixel-perfect design, but flow)
3. **Engineering input**: Which systems are affected? What are technical constraints? Are there dependencies?
4. **Customer evidence**: User research or data validating this is the right approach
5. **Success metrics**: How will we measure if this requirement was met? (Conversion, time on task, support volume, etc.)
6. **Business constraints**: Timeline, resource availability, budget, regulatory requirements

If you're missing key inputs, pause and gather them. A PRD written in a vacuum will be wrong.

## Instructions

### 1. Problem & Context (1 paragraph)

Restate the problem you're solving (link to problem statement). Briefly explain why this solution was chosen over alternatives. This context helps teams understand the "why" and makes tradeoffs visible.

Example:

> Trial users (45% of signups) struggle to share projects with clients because the permissions flow is too complex. Session recordings show 67% of users abandon the invitation flow. This PRD specifies a simplified "Quick Share" flow that lets users share a read-only link with one click, based on user testing showing this is the preferred mental model.

### 2. Success Metrics (Table Format)

Define how you'll measure if the requirement was met. Metrics should be observable and testable.

| Metric                                                | Current   | Target     | Timeframe |
| ----------------------------------------------------- | --------- | ---------- | --------- |
| Trial-to-paid conversion (freelancer segment)         | 8%        | 25%        | Q2        |
| % of users who successfully invite a client by day 14 | 25%       | 50%        | Q2        |
| Support tickets re: client invitations                | 12/month  | <3/month   | Q2        |
| Time to invite first client                           | 8 min avg | <2 min avg | Q2        |

### 3. User Stories or Customer Jobs

Frame requirements in customer context, not technical. Each story should be testable and bounded.

**Format**: As a [user type], I want [action/capability] so that [outcome].

- As a freelance designer, I want to share a read-only link to my project with my client so that they can see progress without needing a login
- As a team lead, I want to set an expiration date on shared links so that access is automatically revoked after the project ends
- As a privacy-conscious user, I want to control what data the client can see (files vs. comments vs. timeline) so that I'm not over-sharing

### 4. Requirements (Detailed)

Break requirements into functional and non-functional categories.

**Functional Requirements** (what the product does):

1. **Quick Share Link Generation**
   - Users can generate a shareable link from any project with one click
   - Link grants read-only access to project files, timeline, and comments (no edit capability)
   - Link includes project name and shared date in the preview (before opening)
   - Links are valid for 30 days by default (customizable by user)

2. **Access Control**
   - Shared link recipients cannot edit, delete, or move files
   - Shared link recipients cannot add/remove collaborators
   - Shared link recipients can add comments (optional; configurable by sharer)
   - Shared link access can be revoked instantly from the project settings

3. **Link Management**
   - Users can see a list of all active shared links on their project
   - Users can edit link settings (expiration, permissions) without regenerating the link
   - Users can view who accessed the link (if analytics are enabled in account settings)

**Non-Functional Requirements**:

- **Performance**: Link generation <200ms; shared link page load <1s on 3G connection
- **Accessibility**: Shared page meets WCAG 2.1 AA standards
- **Security**: Links use URL-safe, cryptographically secure tokens (min 32 bytes entropy); no personally identifiable information in URL
- **Scalability**: System should support 1M concurrent shared links per region

### 5. Edge Cases & Boundaries

Specify what happens outside the happy path. This is where mediocre products diverge from polished ones.

| Edge Case                                       | Behavior                                                                                                 |
| ----------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Shared project is deleted**                   | Shared link returns 404 with message "This project is no longer available"                               |
| **Sharer removes shared link (access revoked)** | Shared link returns 403 with message "Access has been revoked"; user is offered option to request access |
| **Shared link expires**                         | User sees message "This link has expired" with option to contact sharer                                  |
| **Shared project is made private**              | Existing shared links are automatically revoked; sharer is notified                                      |
| **User has no active projects**                 | "Quick Share" button is disabled with tooltip "Create a project first to generate a share link"          |
| **Link accessed from incognito/private mode**   | Works normally; no session creation (follows standard link behavior)                                     |

### 6. Constraints & Assumptions

State what's explicitly out of scope and any constraints that impact design/engineering.

**Technical Constraints**:

- Must use OAuth 2.0 for API authentication; do not reinvent auth
- Link preview must work in email clients (no JavaScript, no complex interactions)
- Shared link pages must not require sign-up (no friction for recipients)

**Business Constraints**:

- Feature must launch within Q2 (hard deadline for sales commitment)
- Shared links are available on all plans (even free)
- No additional server infrastructure is available; must fit in existing Postgres/Redis architecture

**Assumptions**:

- We assume users want read-only sharing by default (based on user testing); write-access sharing is out of scope
- We assume most shares last <30 days (based on usage data); persistent links are out of scope
- We assume enterprise customers will want SSO integration; not in scope for MVP

### 7. Design Specifications (Link to Design Docs)

High-level flow and layout. Detailed design is the design team's job, but PRD should define scope.

**Key Screens**:

- Project detail view: Add "Share" button in top right (near "More options")
- Share modal: Display read-only link, copy button, settings toggle (expiration, permissions)
- Project settings → "Share" tab: List of active links with manage/revoke controls

**Information Architecture**:

- Shared links are project-level, not file-level (reduces complexity for MVP)
- All shared links for a project use the same permissions model

### 8. Success Criteria & Testing

Define how QA will verify the requirement is met. Each acceptance criterion should be testable by a human or automated test.

**Acceptance Criteria**:

- [ ] User can generate a share link from project detail view in <2 clicks
- [ ] Shared link generates in <200ms (measured via performance monitoring)
- [ ] Shared link recipient can view all project files without login
- [ ] Shared link recipient cannot edit, delete, or move files (attempts result in "Read-only" error)
- [ ] Shared link expires after 30 days (links older than 30 days return 403)
- [ ] User can revoke link access; revoked links immediately return 403
- [ ] Shared link works in email clients (tested on Gmail, Outlook, Apple Mail)
- [ ] Page is fully accessible (WCAG 2.1 AA; tested with axe DevTools)
- [ ] No personally identifiable information is exposed in URL or page source
- [ ] System supports 1M concurrent shared links under load (load test: 100 req/sec for 10 min)

## Output Format

A 4-6 page document including:

1. **Executive Summary** (1 paragraph): What problem? Why this solution? Expected business impact?
2. **Problem Statement** (link to discovery doc)
3. **Success Metrics** (table)
4. **User Stories** (5-8 concise stories)
5. **Requirements** (functional + non-functional, organized by feature area)
6. **Edge Cases** (table)
7. **Constraints** (bulleted)
8. **Design Specs** (wireframe links + high-level flow)
9. **Acceptance Criteria** (testable checklist)
10. **Dependencies** (what teams/systems are affected?)
11. **Timeline** (phases: design review, engineering, QA, launch)

## Worked Example

**PRD: Quick Share Links for Freelancer Projects**

**Problem**: Freelancers can't easily share project progress with clients; they currently email status updates manually or give clients login access (security risk). This feature enables read-only sharing via a one-click link.

**Success Metrics**: Trial-to-paid conversion in freelancer segment improves from 8% to 25% within Q2.

**User Stories**:

- As a freelance designer, I want to share a link to my project with my client so that they can see progress without needing a login
- As a freelancer, I want to set an expiration date on shared links so that access is automatically revoked after the project ends
- As a team lead, I want to control what my client can see (files only vs. files + comments) so that I'm not over-sharing work-in-progress

**Key Requirements**:

1. Generate shareable link with one click; read-only by default
2. Link expires after 30 days (customizable by user)
3. Recipients do not need account or password
4. Shared link access can be revoked instantly
5. No PII in URL; cryptographically secure tokens

**Edge Cases**:

- Shared project is deleted → link returns 404
- Link expires → user sees message with option to request access
- User revokes link → link immediately returns 403

**Acceptance Criteria**:

- [ ] User can generate link in <2 clicks
- [ ] Link generation completes in <200ms
- [ ] Recipient can view files without login
- [ ] Recipient cannot edit files (read-only enforced)
- [ ] Link expires after 30 days
- [ ] Revoked links immediately return 403

---

## Decision Framework

When writing a PRD and facing ambiguity:

- **If user story is vague** (e.g., "As a user, I want better performance"): Rewrite with specific context and measurable outcome
- **If you're unsure if something is in scope**: Ask: "Does the customer problem require this?" If no, it's nice-to-have (explicitly mark as out-of-scope)
- **If engineering says "this is hard"**: Don't change the requirement. Ask them to propose a technical approach. If the technical cost is too high, escalate to product leadership to confirm priority.
- **If there's disagreement between design and product on the requirement**: Use the problem statement as north star. Does the requirement solve the customer problem? If both designs solve it equally, defer to design judgment on UX.
- **If you're writing acceptance criteria and think "this is subjective"**: Stop. Make it objective. "Responsive design" is subjective. "Page loads in <1s on 3G and is readable on 320px width" is objective.

## Anti-Patterns & Guards

### Anti-Pattern 1: Solution Prescribing (Not Requirement Defining)

**Description**: "Build a modal dialog with a text input field and a 'Copy' button" instead of "Users must be able to copy the share link to clipboard with one click."

**Why LLMs make this mistake**: LLMs are trained on design specs, not requirements. They optimize for describing solutions, not defining problems and criteria.

**Guard**: If your PRD says "Use X technology" or "Build Y UI component," rewrite it as a requirement. "The component must support..." or "The user must be able to..."

**Example**:

- ❌ Bad: "Add a modal dialog with a dropdown for permissions"
- ✓ Good: "Users must be able to change permissions without regenerating the link. The control must be accessible and support keyboard navigation."

### Anti-Pattern 2: Vague Acceptance Criteria

**Description**: "Link works" or "Feature is performant" (not testable) vs. "Shared link page loads in <1s on 3G and renders correctly at 320px width" (testable).

**Why LLMs make this mistake**: LLMs often default to high-level language that sounds professional but isn't falsifiable.

**Guard**: For every acceptance criterion, ask: "Can a QA engineer or automated test verify this without ambiguity?" If not, rewrite it to be measurable.

**Example**:

- ❌ Bad: "[ ] Link is secure"
- ✓ Good: "[ ] Link uses URL-safe, cryptographically secure tokens (≥32 bytes entropy); no PII in URL or page source"

### Anti-Pattern 3: Missing Edge Cases

**Description**: Writing PRD that specifies happy path only; not thinking through failure modes, boundaries, or data limits.

**Why LLMs make this mistake**: LLMs focus on positive cases because they appear in training data most. Error handling requires deliberate thinking.

**Guard**: For every requirement, ask: "What could go wrong?" and "What happens at boundaries?" Create an edge-case table before handing off to design/engineering.

### Anti-Pattern 4: Disconnected from Problem & Metrics

**Description**: PRD that lists features without explaining why they matter or how you'll measure success.

**Why LLMs make this mistake**: LLMs can generate plausible feature lists without grounding in customer evidence or business context.

**Guard**: Every PRD should have a clear line: Problem → Success Metrics → User Stories → Requirements. If you remove any one, it's incomplete.

### Anti-Pattern 5: No Design Review Before Engineering

**Description**: Handing PRD to engineering without design having reviewed and agreed on scope.

**Why this fails**: Design may have concerns (feasibility, UX coherence) that should be flagged before engineering effort begins. Engineering should not be surprised by requirements.

**Guard**: PRD review gate: Product → Design → Engineering (sequential) before engineering starts building.

## Quality Checklist

Before sharing the PRD:

- [ ] **Evidence-linked**: Problem statement is linked; customer evidence backs the scope
- [ ] **Metrics-focused**: Success metrics are specific, measurable, and testable
- [ ] **User-centric**: User stories frame requirements in customer language, not technical
- [ ] **Solution-free**: Specifies _what_ to build, not _how_ to build it
- [ ] **Constraints clear**: Technical, business, and timeline constraints are explicit
- [ ] **Edge cases covered**: Key failure modes and boundary conditions are documented
- [ ] **Acceptance criteria testable**: Every criterion can be verified by QA or automated test
- [ ] **Design alignment**: Design team has reviewed and agreed on scope
- [ ] **Engineering feasibility**: Engineering has confirmed no blocking technical issues

## Further Reading

- Cagan, Marty. _Inspired: How to Create Products Customers Love_. Wiley, 2008. Chapters 4-6 on product requirements and discovery
- Leffingwell, Dean. _Scaling Software Agility: Best Practices for Large Enterprises_. Addison-Wesley, 2007. On requirements management at scale
- Gilb, Tom. _Competitive Engineering: A Handbook For Systems Engineering, Requirements Engineering, and Software Engineering Using Planguage_. Butterworth-Heinemann, 2005. Chapter on testable specifications
- Gothelf, Jeff and Josh Seiden. _Lean UX: Applying Lean Principles to Improve User Experience_. O'Reilly, 2013. On iterative requirements and feedback
