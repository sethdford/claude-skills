---
name: technical-roadmap
description: Build multi-quarter technical roadmaps aligned with business goals, clearly showing strategic investments, trade-offs, and dependencies. Use when planning longer-term technical direction, communicating with stakeholders, or aligning engineering capacity with business priorities.
allowed-tools: Read, Grep, Glob, Write, Edit
---

# Technical Roadmap Planning

Develop a 3-12 month technical vision that translates business strategy into engineering work, making trade-offs visible and enabling cross-functional alignment.

## Context

You are helping create a technical roadmap that guides engineering work for the next quarter or year. A good roadmap explains not just _what_ you're building, but _why_ it matters to the business and what you're _not_ doing (the trade-offs).

Technical roadmaps fail when they're either too detailed (become outdated) or too vague (don't provide direction). The best roadmaps are strategic narratives, not feature lists.

## Domain Context

- **Camille Fournier's "The Manager's Path"**: Tech leads must translate between business and engineering language
- **Will Larson's "An Elegant Puzzle"**: Roadmaps as three-part narratives: what, why, how we'll get there
- **Tanya Reilly's "The Staff Engineer's Path"**: Owning multi-team technical direction
- **Bidirectional alignment**: Roadmaps emerge from both product strategy AND technical vision
- **Transparency on trade-offs**: Always show what's NOT being done and why
- **Milestone-based, not feature-based**: Organize by quarters with clear outcomes

## When to Use This Skill

- You're starting a new year/quarter and need to plan engineering work
- Business priorities are unclear; you need to ground engineering decisions in strategy
- Teams are working on misaligned initiatives; you need a north star
- Stakeholders ask "Why aren't we doing X?" and you need a clear answer
- You're allocating engineers across multiple projects and need to justify priorities

## Prerequisites

Before building the roadmap, gather:

1. **Product strategy**: What's the business trying to achieve next 12 months?
2. **Team capacity**: How many engineers? What's realistic velocity?
3. **Technical debt**: What's slowing us down? What requires investment?
4. **Platform constraints**: What's blocking teams from shipping fast?
5. **Customer feedback**: What's breaking? What do customers ask for?
6. **Market dynamics**: Are competitors doing something we need to match?

## Instructions

### 1. Gather Inputs

**From Product**:

- Product roadmap (next 3 quarters)
- Customer priorities (what do high-value customers need?)
- Growth targets (what revenue/user goals drive product?)

**From Engineering**:

- Technical debt assessment (database schema, monolith migration, test flakiness)
- Performance bottlenecks (what's slow?)
- Operational load (on-call burden, deployment friction)
- Team bandwidth (realistically, how much capacity?)

**From Leadership**:

- Strategic bets (are we investing in a new market?)
- Hiring plans (will team grow? When?)
- Budget constraints (can we buy solutions or must we build?)

### 2. Define Themes (3-5 Strategic Areas)

Group work into themes that tell a story:

Example themes:

- **Stability**: Reduce production incidents, improve observability
- **Scale**: Handle 10x growth without architectural changes
- **Developer Experience**: Ship features 3x faster (reduce friction)
- **Compliance**: Achieve SOC2 certification
- **Ecosystem**: Build APIs for third-party integrations

Each theme should be ~20-30% of engineering capacity.

### 3. Map Initiatives Within Each Theme

For each theme, list 2-3 major initiatives:

| Theme     | Initiative                                        | Expected Impact                        | Risk                    | Effort (weeks) |
| --------- | ------------------------------------------------- | -------------------------------------- | ----------------------- | -------------- |
| Stability | Migrate from Elasticsearch to managed OpenSearch  | 30% reduction in on-call pages         | Medium (new tool)       | 6              |
| Stability | Add distributed tracing (APM)                     | 50% faster incident diagnosis          | Low                     | 4              |
| Scale     | Refactor user-service monolith                    | Handle 10x growth; improve MTTR        | High (complex refactor) | 12             |
| Scale     | Build caching layer (Redis)                       | 40% reduction in DB queries            | Medium                  | 3              |
| DX        | Improve CI/CD (reduce deploy time from 20m to 5m) | Faster iteration; unblock product team | Low                     | 5              |

### 4. Establish Quarterly Milestones

Break into 3-month cycles with clear outcomes:

**Q1 (Jan-Mar): Foundation**

- Outcome: Observability in place; APM deployed; 80% of services instrumented
- Major work: APM integration, logging standardization, metric collection
- Risk: APM adoption slower than expected (mitigate: dev tutorials, pair sessions)

**Q2 (Apr-Jun): Scale**

- Outcome: Database sharding plan finalized; user-service shards operating in staging
- Major work: User-service monolith refactoring; sharding POC
- Dependency: Caching layer from Q1 must be stable (reduces database load)

**Q3 (Jul-Sep): Hardening**

- Outcome: Compliance audit passed; SOC2 ready; incident response tested
- Major work: Audit controls, RBAC, encryption, incident response tabletops

### 5. Build the Narrative

Write a 1-2 page strategy document:

```
# Engineering Roadmap: 2024

## Strategic Context
Our product is scaling; we've reached 5M daily active users. Our infrastructure
is maxing out:
- Database at 85% capacity
- On-call pages up 40% YoY
- Deploy time is 20 min (slowing product iteration)

To support 10M users and reduce operational burden, we need to invest in:
1. Observability (reduce MTTD/MTTR)
2. Scale (database sharding, caching)
3. Developer velocity (faster deploys, better tooling)

## Q1-Q2 Priorities (50% of capacity)

**Theme: Observability (Q1)**
- Deploy APM (New Relic / DataDog)
- Migrate to managed Elasticsearch (OpenSearch)
- Standardize logging across services
- Expected outcome: 30% reduction in on-call pages; incident diagnosis 2x faster

**Theme: Scale (Q2)**
- Refactor user-service monolith for sharding
- Implement Redis caching layer
- Database sharding plan & POC
- Expected outcome: Ready for 10M users; database queries reduced 40%

## Q3 Priority (30% of capacity)

**Theme: Compliance**
- SOC2 audit preparation
- Implement RBAC
- Encrypt sensitive data at rest
- Expected outcome: SOC2 Type II certification

## Technical Debt (20% of capacity)

- Test flakiness (E2E tests failing 10% of runs)
- CI/CD optimization (deploy time 20m → 5m target)
- Library updates (many dependencies out of date)

## What We're NOT Doing (and why)

- API rate limiting (low demand; competitive advantage is features, not APIs)
- Multi-region deployment (business prioritizes single-region until 2025)
- Event sourcing migration (complex; not critical until we need audit trails)

These could be revisited in 2025 based on business direction.

## Dependencies & Risks

- APM deployment depends on vendor onboarding (4-week lead time; start immediately)
- Sharding depends on cache layer stability (Q1 must complete)
- Compliance audit scheduled for Q3; prep work begins Q2
```

### 6. Identify Cross-Team Dependencies

Map which teams depend on which work:

| Initiative     | Owning Team | Depends On          | Unblocks                     |
| -------------- | ----------- | ------------------- | ---------------------------- |
| APM deployment | Platform    | (none)              | Product (faster deployments) |
| Cache layer    | Backend     | APM (observability) | Scaling work, API team       |
| Sharding       | Backend     | Cache layer         | Scaling to 10M users         |
| RBAC           | Security    | (none)              | Compliance, Product          |

### 7. Set Gates for Reassessment

Define conditions that would trigger roadmap changes:

- **Market change**: Competitor launches feature; business decides we need to match
- **Customer loss**: High-value customer churns due to technical limitation
- **Team attrition**: Engineer leaves; reallocate capacity
- **Business pivot**: Company enters new market; technical priorities shift
- **New constraint**: Regulatory requirement emerges

Roadmap is reviewed quarterly; major changes require stakeholder approval.

## Output Format

A roadmap document (shared with engineering and stakeholders):

```
# 2024 Engineering Roadmap

## High-Level Strategy
[1-2 paragraph context and goals]

## Q1-Q4 Themes & Initiatives
[Table or narrative showing what, why, expected impact]

## Quarterly Breakdown
- **Q1 Focus**: [3-5 key outcomes]
- **Q2 Focus**: [3-5 key outcomes]
- **Q3 Focus**: [3-5 key outcomes]
- **Q4 Focus**: [3-5 key outcomes]

## Technical Debt Allocation
[20-30% of capacity reserved for debt paydown]

## Trade-Offs & What We're NOT Doing
[Explicitly list major initiatives deferred and why]

## Dependencies & Risks
[Cross-team dependencies, technical risks, mitigation]

## Success Metrics
[How do we know the roadmap is working?]

## Reassessment Gates
[Conditions that would trigger roadmap changes]
```

## Worked Example

**Engineering Roadmap: FinTech Payment Platform (2024)**

### Strategic Context

Our payment platform processes $2B annually across 10K SMB customers. We're experiencing:

- 15% YoY growth in transaction volume
- Increasing regulatory pressure (PCI-DSS v4, KYC requirements)
- Customer complaints about slow settlement (T+3, need T+1)
- High on-call burden (3+ incidents/week)

To maintain growth and compliance, engineering will focus on: reliability (reduce incidents), compliance (PCI-DSS v4 + KYC), and speed (T+1 settlement).

### Quarterly Breakdown

**Q1 (Jan-Mar): Reliability & Observability**

- Deploy distributed tracing (APM)
- Implement incident response program
- Reduce on-call alert volume 50%
- Expected outcome: On-call pages drop from 15/week to 8/week

**Q2 (Apr-Jun): Compliance**

- PCI-DSS v4 audit prep (encryption, access controls)
- KYC integration (ID verification, sanctions screening)
- Data retention policies per compliance
- Expected outcome: Pass PCI-DSS v4 audit; KYC launch with first customers

**Q3 (Jul-Sep): Speed**

- Refactor settlement processing (monolith → microservices)
- Real-time clearing (T+1 settlement)
- Merchant dashboard performance improvements
- Expected outcome: T+1 settlement live; customer churn drops 5%

**Q4 (Oct-Dec): Scale & Hardening**

- Database optimization for transaction volume
- Disaster recovery testing (RTO/RPO improvements)
- Compliance hardening (audit controls, logging)
- Expected outcome: Ready for 2025 growth; all compliance controls audited

### Capacity Allocation

- **Core initiatives**: 70% (roadmap items above)
- **Technical debt**: 20% (test flakiness, library updates, CI/CD)
- **Incidents & firefighting**: 10% (buffer for production issues)

### What We're NOT Doing

- **Multi-currency support**: Low demand; complex implementation; deferred to 2025
- **Open banking (PSD2) API**: Regulatory requirement for 2025; starting prep in Q4
- **Blockchain settlement**: Interesting but premature; monitoring market, revisit 2025

### Dependencies

- KYC launch (Q2) depends on APM (Q1) for monitoring third-party API calls
- T+1 settlement (Q3) depends on compliance controls (Q2)
- 2025 scale depends on Q4 disaster recovery improvements

---

## Decision Framework

When building roadmaps and facing uncertainty:

- **If business priorities are unclear**: Push back on product to define top-3 goals. Roadmap without clarity wastes engineering time.
- **If team capacity is unknown**: Assume 60-70% on roadmap work; reserve rest for debt and incidents.
- **If you have more ideas than capacity**: That's healthy. Explicitly defer non-essential work; explain why in "What We're NOT Doing."
- **If a quarter becomes overloaded**: Pause new work; reset expectations; move items to next quarter.

## Anti-Patterns & Guards

### Anti-Pattern 1: Treating Roadmap as Commitment

**Description**: Roadmap listed as firm promises; business commits to customers; engineering fails to deliver.

**Guard**: Frame as "plans if no blocking risks emerge." Roadmaps are bets, not guarantees. Revisit quarterly.

### Anti-Pattern 2: Ignoring Technical Debt

**Description**: Roadmap 100% feature work; technical debt accumulates; velocity drops to zero.

**Guard**: Reserve 20-30% for debt paydown explicitly. Show it as line item in roadmap.

### Anti-Pattern 3: No Explanation of Alternatives

**Description**: Roadmap doesn't explain why Feature X was chosen over Feature Y.

**Guard**: "Alternatives Considered" section showing trade-offs between competing options.

### Anti-Pattern 4: Roadmap Disconnected from Hiring

**Description**: Roadmap assumes team size that won't happen (no hiring plan).

**Guard**: Cross-check roadmap against headcount forecast. If mismatch, either reduce scope or increase hiring.

### Anti-Pattern 5: Changing Roadmap Monthly

**Description**: Roadmap updated constantly; becomes useless as planning tool.

**Guard**: Quarterly review only. Mid-quarter changes require escalation to leadership.

## Quality Checklist

Before sharing the roadmap:

- [ ] **Context clear**: Why are these priorities strategic? How do they serve business goals?
- [ ] **Trade-offs visible**: What's NOT being done and why?
- [ ] **Capacity realistic**: 60-70% on roadmap, 20-30% debt, 10% buffer
- [ ] **Dependencies explicit**: Cross-team dependencies mapped; risk mitigations noted
- [ ] **Outcomes measurable**: Each initiative has clear success criteria
- [ ] **Alternatives considered**: Why this roadmap vs. others?
- [ ] **Hiring implications**: Team size assumptions clear
- [ ] **Reassessment plan**: When/how will roadmap be revisited?

## Further Reading

- Larson, Will. _An Elegant Puzzle: Systems of Engineering Management_. 2019. Chapters on roadmapping.
- Fournier, Camille. _The Manager's Path_. 2017. Chapters on leveraging as tech lead.
- Reilly, Tanya. _The Staff Engineer's Path_. 2022. Chapters on technical direction across teams.
