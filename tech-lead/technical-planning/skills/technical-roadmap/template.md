# Technical Roadmap Template

## High-Level Strategy

[1-2 paragraphs providing strategic context]

- **Current state**: [What's the status quo? What's working? What's strained?]
- **Business drivers**: [Why does the business care about these technical investments?]
- **Strategic goals**: [What outcomes should this roadmap enable?]

---

## Quarterly Breakdown

### Q[X] [Theme/Focus]

**Outcome**: [What's the measurable outcome for this quarter?]

**Major Initiatives**:

- [Initiative 1]: [Brief description, expected impact]
- [Initiative 2]: [Brief description, expected impact]
- [Initiative 3]: [Brief description, expected impact]

**Dependencies**: [What must be true from previous quarter?]

**Risks**: [What could go wrong?]

---

## Themes & Capacity Allocation

| Theme                      | Capacity    | Key Initiatives          | Expected Impact            |
| -------------------------- | ----------- | ------------------------ | -------------------------- |
| [Theme 1: e.g., Stability] | [% of team] | [3-5 initiatives]        | [What improves?]           |
| [Theme 2: e.g., Scale]     | [% of team] | [3-5 initiatives]        | [What improves?]           |
| [Theme 3: e.g., Velocity]  | [% of team] | [3-5 initiatives]        | [What improves?]           |
| **Technical Debt**         | [% of team] | [Debt paydown items]     | [Improved maintainability] |
| **Buffer**                 | [% of team] | [Incidents, emergencies] | [Stability]                |

**Total**: Should equal 100% (typically: 60-70% roadmap, 20-30% debt, 10% buffer)

---

## Initiative Detail

| Initiative        | Owning Team | Effort (weeks)  | Expected Impact      | Risk              | Status                    |
| ----------------- | ----------- | --------------- | -------------------- | ----------------- | ------------------------- |
| [Initiative name] | [Team]      | [Time estimate] | [Metric improvement] | [High/Medium/Low] | [New/In Progress/Blocked] |

---

## Cross-Team Dependencies

| Initiative     | Depends On              | Unblocks                     | Timeline |
| -------------- | ----------------------- | ---------------------------- | -------- |
| [Initiative A] | [Initiative B complete] | [Initiative C, Product team] | [Q date] |

---

## Technical Debt Allocation

[20-30% of capacity reserved for debt paydown]

**Examples**:

- [ ] Test flakiness (E2E tests failing X% of runs)
- [ ] Library updates (dependencies out of date)
- [ ] CI/CD optimization (deploy time X min → Y min target)
- [ ] Schema migration (legacy patterns blocking scale)

**Success criteria**: [What should debt metrics look like by end of roadmap period?]

---

## What We're NOT Doing (and Why)

**Explicitly deferred initiatives**:

- [ ] [Initiative]: [Reason for deferral - market prioritization, technical readiness, capacity, etc]
- [ ] [Initiative]: [Reason for deferral]
- [ ] [Initiative]: [Reason for deferral]

These could be revisited in [future period] based on [business direction / technical readiness / customer feedback].

---

## Success Metrics

| Metric     | Current    | Target   | Why This Matters           |
| ---------- | ---------- | -------- | -------------------------- |
| [Metric 1] | [Baseline] | [Target] | [Business/technical value] |
| [Metric 2] | [Baseline] | [Target] | [Business/technical value] |
| [Metric 3] | [Baseline] | [Target] | [Business/technical value] |

---

## Risks & Mitigations

| Risk               | Likelihood | Impact        | Mitigation              |
| ------------------ | ---------- | ------------- | ----------------------- |
| [Risk description] | [H/M/L]    | [Consequence] | [How we prevent/handle] |

---

## Reassessment Gates

**Conditions that would trigger roadmap changes:**

- [ ] [Business pivot or market change]: Requires stakeholder approval
- [ ] [Customer loss]: If high-value customer churns due to technical limitation
- [ ] [Team attrition]: Engineer leaves; reallocate capacity
- [ ] [New constraint]: Regulatory requirement or vendor change emerges
- [ ] Quarterly review: Formal checkpoint for all roadmaps

---

## Hiring Assumptions

- **Current team size**: [N engineers]
- **Projected additions**: [N engineers by month X]
- **Impact on roadmap**: [If no new hires, which initiatives are at risk?]

If hiring plan changes, roadmap must be re-prioritized.

---

## Document Metadata

| Property         | Value                   |
| ---------------- | ----------------------- |
| Owner            | [Tech Lead name]        |
| Created          | [Date]                  |
| Last Updated     | [Date]                  |
| Review Frequency | [Quarterly]             |
| Stakeholders     | [PM, Eng Lead, Finance] |

---

## Sign-Off

- [ ] Engineering Lead approval: ********\_******** Date: **\_\_\_**
- [ ] Product Lead approval: ********\_******** Date: **\_\_\_**
- [ ] Executive Sponsor approval: ********\_******** Date: **\_\_\_**
