# Feature Lifecycle

Maps the full lifecycle of a feature from idea through production monitoring. Explicitly shows each role's contribution at each phase.

## Domain Context

A feature doesn't live in isolation. It moves through distinct phases, and at each phase, a different role takes the lead:

| Phase        | Primary Role                    | Input                            | Output                                                     | Exit Criteria                      |
| ------------ | ------------------------------- | -------------------------------- | ---------------------------------------------------------- | ---------------------------------- |
| Ideation     | Product Manager                 | User problem, business goal      | Problem statement, roadmap prioritization                  | Feature approved for requirements  |
| Requirements | Product Manager + Architect     | Problem statement, constraints   | User stories, acceptance criteria, success metrics         | Requirements complete (DoR)        |
| Design       | Architect + Security + Designer | Requirements, constraints        | Architecture docs, design mockups, threat model            | Design approved                    |
| Development  | Engineer                        | Design, DoR acceptance criteria  | Code, unit tests, implementation docs                      | Code review passed, tests green    |
| Testing      | QA + Engineer                   | Design, implementation           | Test cases, test results, bug reports                      | Test coverage met, bugs resolved   |
| Deployment   | Tech Lead + Engineer            | Tested code, runbook, monitoring | Deployment pipeline, rollback procedure, monitoring alerts | Deployed to production             |
| Operations   | Tech Lead                       | Running feature in production    | Logs, metrics, incidents, customer feedback                | Stable, no critical issues         |
| Closure      | Product Manager + Tech Lead     | Operational stability, metrics   | Retrospective, lessons learned, backlog improvements       | Feature documented, team debriefed |

The feature lifecycle is not linear. It may:

- Loop back (design issue found during development → redesign → reimplement)
- Iterate (deploy v1 → get feedback → plan v2 improvements)
- Split (feature splits into multiple parallel epics)

**ISO/IEC 12207 Reference:**

- 5.2.1 Stakeholder Needs and Requirements Definition
- 5.3 Technical Processes (design, implementation, verification, transition, operation)

## Instructions

### Step 1: Establish Feature Context

- **Input**: Feature name, problem statement, business goal
- **Ask**: Who's the primary PM? Architect? Security lead?
- **Ask**: What's the approximate scope? (small feature, large epic, infrastructure)
- **Ask**: Are there known constraints? (timeline, security, performance, compatibility)

### Step 2: Ideation Phase

- **PM**: Articulates problem, potential solutions, business value
- **Output**: Problem statement, initial roadmap prioritization
- **Next**: Send to requirements planning

### Step 3: Requirements Phase

- **PM**: Writes user stories, acceptance criteria, success metrics
- **Architect**: Assesses feasibility, identifies design complexity, dependency risks
- **Security**: Identifies threat surface, required security controls
- **Designer**: Scopes UX work, design systems integration
- **Tech Lead**: Estimates effort, identifies team skills, deployment strategy

Use `/sdlc:definition-of-ready` to validate requirements completeness

- **Output**: Requirements document (user stories, success metrics, acceptance criteria, DoR checklist)
- **Exit**: All DoR criteria met; ready to move to design

### Step 4: Design Phase

- **Architect**: Decomposes system into components, documents trade-offs, creates architecture diagrams
- **Security**: Creates threat model (STRIDE), identifies mitigations, scopes security testing
- **Designer**: Creates wireframes, mockups, interaction patterns, accessibility plan
- **Engineer**: Participates in design review, identifies implementation risks
- **Tech Lead**: Reviews design for operational implications (monitoring, logging, scaling)

Use `/sdlc:design-review` to validate design cross-functionally

- **Output**: Design document (architecture, threat model, mockups, accessibility plan, trade-offs)
- **Exit**: Design approved by architect, security, designer; no blocking issues

### Step 5: Development Phase

- **Engineer**: Implements code following the design, writes unit tests, participates in code reviews
- **QA**: Works with engineer on test strategy, preps test cases
- **Tech Lead**: Ensures code is maintainable, reviews code organization
- **Designer**: Ensures implementation matches design; flags mismatches

Use `/sdlc:quality-gate` to validate implementation meets design and code standards

- **Output**: Working code with unit tests, code review, implementation documentation
- **Exit**: Code review passed, unit tests passing, DoD implementation criteria met

### Step 6: Testing Phase

- **QA**: Executes test strategy, reports bugs, validates fixes
- **Engineer**: Fixes bugs, works with QA on edge cases
- **Security**: Runs SAST/DAST scans, validates security controls
- **Designer**: Validates UI/UX match design on real implementation

Use `/sdlc:quality-gate` again to validate testing is complete

- **Output**: Test results, bug reports, security scan results
- **Exit**: All test cases passed, bugs fixed, security scan passed, test coverage adequate

### Step 7: Deployment Phase

- **Tech Lead**: Orchestrates deployment, ensures rollback procedure is ready
- **Engineer**: Executes deployment steps, monitors for anomalies
- **Operations**: Monitors system health, readies for incident response
- **PM**: Prepares release communications, customer notifications

Use `/sdlc:release-checklist` to validate deployment readiness

- **Output**: Feature deployed to production, monitoring active, incidents ready
- **Exit**: Feature stable in production, no critical alerts, team trained

### Step 8: Operations Phase

- **Tech Lead**: Monitors feature health, responds to incidents
- **Engineer**: Responds to bugs, works on post-launch improvements
- **PM**: Collects user feedback, observes success metrics
- **Security**: Monitors for security anomalies

Duration: Minimum 1-2 weeks; until stability is confirmed

- **Output**: Operational metrics, incident reports, user feedback
- **Exit**: Feature meets success metrics, no critical issues, team confident in stability

### Step 9: Closure Phase

- **PM**: Validates success metrics, gathers user feedback, plans follow-up improvements
- **Tech Lead**: Facilitates retrospective, documents lessons learned
- **Engineer**: Archives technical docs, identifies debt to address
- **Security**: Reviews security incidents (if any), updates threat model if needed

Use `/sdlc:retrospective-to-action` to consolidate learnings

- **Output**: Retrospective document, action items, lessons learned, feature tagged as stable
- **Exit**: Feature is documented, team debriefed, backlog has follow-up items if needed

### Step 10: Document the Feature Lifecycle

Create a feature lifecycle document:
```

Feature: [Name]
Problem: [User problem being solved]
Business Goal: [Expected impact]
Timeline: [Estimated dates for each phase]

Ideation: [PM drive, dates, decisions]
Requirements: [Stories, success metrics, DoR]
Design: [Architecture, threats, mockups, DoD]
Development: [Code, tests, documentation]
Testing: [Test results, bugs, fixes]
Deployment: [Release plan, rollback procedure]
Operations: [Stability period, incidents, metrics]
Closure: [Retrospective, lessons learned, follow-ups]

Key Milestones:

- Requirements approved: [date]
- Design approved: [date]
- Code complete: [date]
- Testing approved: [date]
- Production deployment: [date]
- Stability confirmed: [date]

Role Contributions:

- PM: Requirements, go/no-go decisions, success metric validation
- Architect: Design, trade-off analysis, scaling/performance review
- Security: Threat modeling, security testing, vulnerability management
- Engineer: Implementation, code quality, testing, deployment
- QA: Test strategy, test execution, bug triage
- Designer: UX design, accessibility, design system consistency
- Tech Lead: Orchestration, documentation, operational readiness

Post-Launch Actions: [Follow-up items, technical debt, process improvements]

```

## Anti-Patterns

1. **Skipping the operations phase**
   - Mistake: "Feature is deployed, we're done"
   - Correct: Operations phase confirms stability; only then is it "done"
   - Fix: Require minimum 1-2 weeks of monitoring before closure

2. **Not looping back on design issues found during development**
   - Mistake: "The design says do X, but it doesn't work, so let's hack around it"
   - Correct: Design issues should trigger a design redesign, not implementation hacks
   - Fix: When development hits design issues, pause and redesign before implementing

3. **Skipping the designer throughout the lifecycle**
   - Mistake: "Designer was involved at the start, now engineering owns it"
   - Correct: Designer reviews implementation against design; catches mismatches early
   - Fix: Designer is involved in design phase → development QA → launch verification

4. **Not including security until testing phase**
   - Mistake: "Security review happens at the end"
   - Correct: Security is part of design (threat modeling); testing phase is too late
   - Fix: Security designs threat model in design phase; testing phase validates mitigations

5. **Treating closure as optional**
   - Mistake: "We shipped it, closing the ticket now"
   - Correct: Closure requires retrospective and lessons learned
   - Fix: Require closure ceremony; capture learnings for future features

## Further Reading

- **ISO/IEC 12207** — Software lifecycle processes
- **Agile Release Train** — SAFe, Program Increment Planning (https://www.scaledagileframework.com/)
- **Feature Lifecycle** — Reinertsen, D., "The Principles of Product Development Flow" (Celeritas Publishing)