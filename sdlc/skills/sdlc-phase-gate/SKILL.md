# SDLC Phase Gate

Validates that work meets criteria before moving between SDLC phases. Implements gates for: Requirements → Design → Implementation → Testing → Deployment → Operations.

## Domain Context

Software lifecycle is a series of phases, each with distinct concerns and responsibilities:

| Phase          | Primary Role         | Key Questions                                         |
| -------------- | -------------------- | ----------------------------------------------------- |
| Requirements   | Product Manager      | What problem are we solving? Is it worth solving?     |
| Design         | Architect            | How will we solve it? What are the risks?             |
| Implementation | Engineer             | Can we actually build this?                           |
| Testing        | QA                   | Does it work as designed?                             |
| Deployment     | Tech Lead / Engineer | Is the rollout safe? Can we roll back?                |
| Operations     | Tech Lead            | Is it stable in production? Can we respond to issues? |

A phase gate ensures that before moving to the next phase, the current phase is sufficiently complete and the next phase has what it needs.

Phase gates are **guardrails**, not bureaucratic checkpoints. They catch misalignment early, when changes are cheap.

**ISO/IEC 12207 Reference:**

- 5.2.1 Stakeholder Needs and Requirements Definition
- 5.3.1 System Requirements Analysis
- 5.3.3 Architectural Design
- 5.3.4 Detailed Design
- 5.3.5 Implementation
- 5.3.6 Integration
- 5.3.7 Verification
- 5.3.8 Transition
- 5.3.9 Operation and Maintenance

## Instructions

### Step 1: Identify Current Phase and Work Item

- **Input**: Work item (feature, task, epic, release)
- **Ask**: What phase is this in? (Requirements, Design, Implementation, Testing, Deployment, Operations)
- **Ask**: What's the scope? (feature, bug fix, infrastructure, tech debt)

### Step 2: Validate Current Phase Completion

For **Requirements → Design Gate**:

- Is the problem statement clear and agreed by all stakeholders?
- Is the success metric defined and measurable?
- Have edge cases and failure modes been identified?
- Has the security threat landscape been scoped?
- Is the scope bounded (no hidden assumptions)?

Output: Requirements completeness checklist

For **Design → Implementation Gate**:

- Has the system architecture been decomposed into components?
- Have trade-offs been explicitly documented (performance vs. complexity, flexibility vs. cost)?
- Has the security architecture been threat-modeled (STRIDE or equivalent)?
- Have dependency risks been identified (external services, rate limits, SLAs)?
- Has the accessibility design been reviewed?
- Is the design reviewable and approved by architect and security?

Output: Design completeness checklist

For **Implementation → Testing Gate**:

- Is the code complete for the feature (or slice)?
- Does the code follow team conventions and pass static analysis?
- Have unit tests been written and pass?
- Has the test strategy been defined (what will QA validate)?
- Are deployment rollback procedures documented?
- Have performance baselines been captured?

Output: Implementation readiness checklist

For **Testing → Deployment Gate**:

- Have all test scenarios passed (happy path, edge cases, error cases)?
- Has the test coverage met the team's threshold?
- Have security scans passed (SAST, dependency audit, secrets scan)?
- Have accessibility tests passed (WCAG, screen reader, keyboard navigation)?
- Have performance benchmarks met targets?
- Is the rollback procedure tested and documented?

Output: Testing completeness checklist

For **Deployment → Operations Gate**:

- Is the deployment plan approved by tech lead and ops?
- Is the rollout strategy clear (blue-green, canary, gradual)?
- Are monitoring and alerting configured?
- Is the runbook written (how to debug in production)?
- Have team members been trained on the feature?
- Is the incident response plan ready?

Output: Deployment readiness checklist

For **Operations → Closure Gate**:

- Is the feature stable in production (no critical alerts)?
- Are the monitoring metrics showing expected behavior?
- Have incident reports been reviewed and closed?
- Are there improvement items from operations feedback?
- Can the team move on to the next feature?

Output: Operations closure checklist

### Step 3: Identify Blocking Issues

For each failed criterion:

- **What's missing?** (artifact, approval, test, documentation)
- **Who owns fixing it?** (architect, engineer, PM, security, QA, designer)
- **How long to fix?** (estimate in hours)
- **Does it block the phase transition?** (blocking, warning, informational)

Output: Blocking issues list with owners and estimates

### Step 4: Make the Gate Decision

**Go Decision:**

- All blocking criteria are satisfied
- No critical risks remain unmitigated
- Next phase team has what it needs to succeed
- Document: "Gate approved, ready to transition"

**Conditional Go Decision:**

- Critical criteria are satisfied
- Non-critical criteria have acceptable workarounds
- Risk is documented and accepted
- Document: "Gate approved with accepted risks: [list]"

**No-Go Decision:**

- Critical criteria are not satisfied
- Risks cannot be mitigated in the next phase
- Recommend: Fix the issue in current phase
- Document: "Gate blocked. Required fixes: [list]. Re-evaluate in [timeframe]"

### Step 5: Communicate the Decision

- **To Current Phase Team**: "Gate decision is [go/conditional/no-go]. [Issues to fix]. [Next steps]."
- **To Next Phase Team**: "You're cleared to proceed. Here's what you're inheriting: [scope, risks, dependencies]."
- **To Leadership**: "Feature [X] is [on track / at risk] for [target date]. Blocker: [if any]."

## Anti-Patterns

1. **Using phase gates to rubber-stamp completion**
   - Mistake: "All checkboxes are checked, so the gate passes automatically"
   - Correct: Checklists inform the decision, but the decision is a judgment call
   - Fix: Require explicit human sign-off for go/no-go decisions

2. **Making gates too early in the phase**
   - Mistake: "Let's do the testing gate after the first sprint of development"
   - Correct: Gates should be at natural phase boundaries, when work is substantially complete
   - Fix: Define phase boundaries clearly; gate when "done" is achievable

3. **Skipping gates because "we're fast"**
   - Mistake: "Agile teams don't need phase gates, we ship continuously"
   - Correct: Continuous delivery still needs guardrails; gates work at sprint granularity
   - Fix: Apply phase gates to features or epics, not individual PRs

4. **Treating gates as single-role decisions**
   - Mistake: "The architect decides if design is complete"
   - Correct: Design completeness requires architect + security + engineer input
   - Fix: Make gates cross-functional; require sign-off from the role entering the phase

5. **Not capturing risk and context**
   - Mistake: "Gate passed, move on" (without documenting assumptions or risks)
   - Correct: Gate decisions should capture trade-offs and accepted risks
   - Fix: Always document: "This decision assumes [X]. If [Y] changes, re-evaluate."

6. **Gates that are too strict**
   - Mistake: "100% test coverage required; gates don't pass without it"
   - Correct: Thresholds should be evidence-based, not arbitrary
   - Fix: Define thresholds based on team data (velocity, defect rates, severity)

## Further Reading

- **ISO/IEC 12207** — Software lifecycle processes (Section 5.2, Process implementation)
- **Stage-Gate Process** — Cooper, R. G., "Winning at New Products" (Harvard Business Review Press)
- **Lean Phase Gates** — Reinertsen, D., "The Principles of Product Development Flow" (Celeritas Publishing)
- **Risk Management in Phase Gates** — PMI, "Project Management Institute Body of Knowledge" (PMBOK)