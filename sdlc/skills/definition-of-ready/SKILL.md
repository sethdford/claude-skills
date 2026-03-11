# Definition of Ready

Ensures work items are ready for development before sprint intake. Combines PM requirements skills + architect design feasibility + security threat assessment.

## Domain Context

A team's velocity (or lack thereof) is often determined not by how fast engineers code, but by how often they're blocked waiting for clarification, design direction, or security sign-off.

**Definition of Ready** (DoR) is a collective agreement about what information a work item must have before it can be brought into a sprint. It's not a checklist to optimize away; it's an investment that accelerates the entire team.

**Who owns DoR?**

- **Product Manager** — Writes clear problem statements, acceptance criteria, success metrics
- **Architect** — Confirms design feasibility, identifies complexity hotspots
- **Security** — Identifies threat surface, required security design
- **Designer** — Assesses UX implications and design work required
- **Tech Lead** — Estimates complexity, identifies dependencies

A work item is "ready" when the team that will execute it has everything needed to execute efficiently.

**ISO/IEC 12207 Reference:**

- 5.2.1 Stakeholder Needs and Requirements Definition
- 5.3.1 System Requirements Analysis (feasibility assessment)

## Instructions

### Step 1: Collect the Work Item

- **Input**: Work item (story, feature, task, spike)
- **Ask**: What's the title, description, acceptance criteria?
- **Ask**: Who wrote it? Is it from a user request, roadmap, technical debt, or incident?

### Step 2: PM Perspective — Problem Statement and Acceptance Criteria

Check:

- **Problem Statement**: Is the "why" clear? (Who has the problem? What's the impact?)
- **Success Metric**: Can we measure success? (e.g., "reduce checkout time to <2s", "eliminate class of bugs")
- **Acceptance Criteria**: Are the requirements specific and testable? (Not vague like "improve performance")
- **Out of Scope**: Are assumptions and boundaries clear? (What's NOT included?)
- **Dependencies**: Are external dependencies identified? (API contracts, third-party services, data sources)
- **Stakeholders**: Who needs to sign off? (PM, architect, security, designer)

Output: Requirements completeness checklist

### Step 3: Architect Perspective — Design Feasibility

Check:

- **Is the approach feasible?** Does it fit the existing architecture? (Or require architectural change?)
- **Design Complexity**: What's the complexity tier? (Trivial, simple, moderate, complex)
- **Dependencies**: Are there internal dependencies or integration points?
- **Performance**: Will this meet performance targets?
- **Scalability**: Will this scale to expected load?
- **Integration Points**: Are all integrations identified and scoped?

Output: Feasibility assessment

### Step 4: Security Perspective — Threat Assessment

Check:

- **Threat Surface**: What new security boundaries does this create?
- **Authentication/Authorization**: Are access controls needed?
- **Data Sensitivity**: Is PII, secrets, or regulated data involved?
- **Third-Party Risk**: Are we calling external services? Trusted?
- **Compliance**: Does this touch regulated domains (payments, health, finance)?
- **Design Review**: Has security architecture been sketched?

Output: Security threat assessment

### Step 5: Designer Perspective — UX and Accessibility

Check:

- **User Flows**: Are the user flows clear? (Happy path, error cases)
- **Design Mockups**: Are there design artifacts? (Wireframes, prototypes)
- **Accessibility**: Are accessibility requirements documented? (WCAG 2.1 AA minimum)
- **Content**: Is copy/messaging clear and reviewed?
- **Interactions**: Are complex interactions documented?

Output: Design feasibility assessment

### Step 6: Tech Lead Perspective — Complexity and Effort

Check:

- **Effort Estimate**: Can the team estimate this? (If not, it's a spike)
- **Team Skills**: Does the team have the skills? (Or need training, hiring, or pairing?)
- **Testing Strategy**: Is the test strategy clear?
- **Deployment Risk**: Is this low-risk (feature flag, new code) or high-risk (shared libraries, data migrations)?

Output: Effort and complexity estimate

### Step 7: Consolidate the DoR Checklist
```

DoR Checklist for [Work Item ID]: [Title]

[ ] PM
[ ] Problem statement is clear
[ ] Success metric is defined and measurable
[ ] Acceptance criteria are specific and testable
[ ] Out-of-scope items are documented
[ ] Dependencies are identified
[ ] Stakeholders identified

[ ] Architect
[ ] Approach is feasible within existing architecture
[ ] Complexity tier is assigned
[ ] Internal dependencies identified
[ ] Performance targets understood
[ ] Integration points scoped

[ ] Security
[ ] Threat surface identified
[ ] Auth/authz requirements documented (if needed)
[ ] Data sensitivity classified
[ ] Third-party risk assessed
[ ] Compliance impact assessed
[ ] Security design reviewed

[ ] Designer
[ ] User flows documented
[ ] Design artifacts exist (mockups/prototypes)
[ ] Accessibility requirements documented
[ ] Copy/messaging reviewed

[ ] Tech Lead
[ ] Effort can be estimated
[ ] Team has required skills (or pairing plan exists)
[ ] Test strategy is documented
[ ] Deployment strategy is clear

Ready? [ ] Yes (all boxes checked) [ ] No (see blocking issues below)

```

### Step 8: Identify Blocking Issues

For each unchecked box:
- **What's missing?** (artifact, clarity, decision, design)
- **Who provides it?** (PM, architect, security, designer, tech lead)
- **How long to fix?** (estimate in hours or days)

Blocking issues prevent the work item from entering the sprint.

### Step 9: Communicate Ready/Not Ready

**Ready Decision:**
- All boxes are checked
- No blocking issues remain
- Document: "Ready to intake into sprint [X]. Assigned to [engineer/team]. Est. [effort]. Start date: [date]."

**Not Ready Decision:**
- Blocking issues exist
- Document: "Not ready. Blockers: [list]. Required actions: [list]. Re-evaluate on [date]."

## Anti-Patterns

1. **DoR as a bottleneck**
   - Mistake: "PM must fill out a 50-field form before anything is ready"
   - Correct: DoR should be lightweight and focused on unblocking the team
   - Fix: Define 5-7 essential questions; everything else is detail

2. **DoR only applies to features, not bugs or tech debt**
   - Mistake: "Bugs are ready immediately; no DoR needed"
   - Correct: Even bugs benefit from clarity on root cause, reproduction, and priority
   - Fix: Lightweight DoR for bugs: "Reproduction steps, severity, affected users, architect approval if cross-team impact"

3. **Skipping the security review because "it's internal"**
   - Mistake: "We're only changing internal APIs, so no security risk"
   - Correct: Internal code paths are attack vectors; threat model always
   - Fix: Always include security in DoR; they can sign off in 30 min for low-risk items

4. **DoR that's static and never evolves**
   - Mistake: "We defined DoR in 2019 and never changed it"
   - Correct: DoR should evolve with team maturity, incident learnings, and tooling
   - Fix: Retro question: "Should we add or remove anything from DoR?"

5. **Using DoR as an excuse to ship incomplete planning**
   - Mistake: "DoR is checked, so we're done planning"
   - Correct: DoR is the minimum; complex work still needs detailed design and spike time
   - Fix: For complex items, plan spike time to reduce design uncertainty

6. **Not using DoR to predict problems**
   - Mistake: "DoR is just paperwork"
   - Correct: DoR should surface risks and misalignment before coding starts
   - Fix: Ask after each sprint: "Which DoR items would have prevented our recent bugs?"

## Further Reading

- **Scrum Guide** — Schwaber, K. & Sutherland, J., Definition of Ready (https://scrumguides.org/)
- **Agile Requirements** — Cohn, M., "User Stories Applied" (Addison-Wesley)
- **Work Item Templates** — SAFe, "Lean Portfolio Management" (https://www.scaledagileframework.com/)