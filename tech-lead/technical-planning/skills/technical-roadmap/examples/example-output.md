# Example: 2026 Engineering Roadmap - FinTech Payment Platform

## High-Level Strategy

Our payment platform processes $2B annually across 10K SMB customers. We're experiencing 15% YoY growth in transaction volume, but our infrastructure is straining:

- Database at 85% capacity (outages in peak hours)
- On-call pages up 40% YoY (team burnout risk)
- Deploy time is 20 minutes (blocking product iteration)
- Regulatory pressure increasing (PCI-DSS v4, GDPR, local KYC requirements)

To maintain growth and stay competitive, engineering will focus on **reliability** (reduce incidents), **compliance** (meet regulations), and **velocity** (ship faster). We'll invest in observability, infrastructure scaling, and regulatory controls.

---

## Quarterly Breakdown

### Q1 (Jan-Mar): Reliability & Observability Foundation

**Outcome**: Reduce MTTD/MTTR by 50%; improve on-call experience; gain operational visibility.

**Major Initiatives**:

- Deploy distributed tracing (APM) across all services
- Implement incident response program (runbooks, tabletop exercises)
- Migrate from Elasticsearch to managed OpenSearch (reduce ops burden)
- Standardize logging across services (structured JSON logs)

**Expected Impact**:

- On-call pages: 15/week → 8/week (53% reduction)
- MTTD: 30 min → 10 min (3x improvement)
- MTTR: 2 hours → 30 min (4x improvement)

---

### Q2 (Apr-Jun): Compliance & KYC Integration

**Outcome**: Pass PCI-DSS v4 audit; launch KYC for new customers; reduce regulatory risk.

**Major Initiatives**:

- PCI-DSS v4 audit preparation (encryption, access controls, key management)
- KYC integration (ID verification, sanctions screening via third-party)
- Data retention policies (GDPR-compliant automatic deletion)
- Compliance monitoring dashboard (detect policy violations)

**Expected Impact**:

- PCI-DSS v4 certification (business blocker for enterprise customers)
- KYC launch for new customer tiers (revenue unlock: +$100K MRR potential)
- Regulatory confidence: Customer NPS +5 points

---

### Q3 (Jul-Sep): Scale & Performance

**Outcome**: Database scaling foundation; ready for 10x growth; reduced latency.

**Major Initiatives**:

- User service monolith refactoring (prepare for sharding)
- Redis caching layer (reduce database load 40%)
- Database sharding POC (test sharding architecture in staging)
- Transaction settlement processing optimization (reduce query time)

**Expected Impact**:

- Database queries: 200ms avg → 50ms avg (4x faster)
- Database load: 85% → 40% capacity
- Ready to handle 10M daily transactions (vs. current 1M)

---

### Q4 (Oct-Dec): Hardening & 2027 Prep

**Outcome**: Incident response tested; disaster recovery validated; 2027 roadmap finalized.

**Major Initiatives**:

- Disaster recovery testing (RTO/RPO validation)
- Security hardening (RBAC enforcement, audit logging completion)
- Performance testing at scale (load testing for Q3 infrastructure)
- 2027 roadmap planning (multi-region deployment, fintech-specific features)

**Expected Impact**:

- Tested RTO: <2 hours (business continuity certified)
- Security controls: 100% audit-ready
- Performance baseline: Known limits for 2027 scaling

---

## Themes & Capacity Allocation

| Theme                | Capacity | Key Initiatives                        | Expected Impact                         | Owner             |
| -------------------- | -------- | -------------------------------------- | --------------------------------------- | ----------------- |
| **Reliability**      | 25%      | APM, incident response, logging        | MTTD/MTTR 3-4x improvement              | Sarah (Infra)     |
| **Compliance**       | 25%      | PCI-DSS v4, KYC, data retention        | Audit pass, regulatory de-risk          | James (Security)  |
| **Scale**            | 30%      | DB sharding, caching, refactoring      | 4x query performance, handle 10x growth | Michael (Backend) |
| **Technical Debt**   | 15%      | Test flakiness, library updates, CI/CD | Reduced maintenance burden              | All               |
| **Incidents/Buffer** | 5%       | Production firefighting                | Stability                               | All               |
| **Total**            | **100%** |                                        |                                         |                   |

---

## Cross-Team Dependencies

| Initiative        | Depends On                         | Unblocks                           | Timeline   |
| ----------------- | ---------------------------------- | ---------------------------------- | ---------- |
| APM deployment    | Vendor onboarding (4 weeks)        | Faster incident response (all Q2+) | Week 3 Q1  |
| KYC integration   | APM (monitoring third-party calls) | Revenue unlock, new customer tiers | Week 8 Q1  |
| DB caching layer  | APM (performance baselines)        | Sharding POC (Q3)                  | Week 6 Q1  |
| Sharding POC      | Caching stable (Q1 complete)       | Production sharding (2027)         | Week 12 Q2 |
| Disaster recovery | Infrastructure hardened (Q3)       | 2027 multi-region roadmap          | Week 48 Q4 |

---

## Technical Debt Allocation

**15% capacity reserved for debt paydown (3 engineers equivalent)**

### Q1 Debt Work

- Test flakiness: E2E tests failing 8% of runs → target 2%
- Library updates: 47 dependencies >6 months old
- CI/CD: Reduce deploy time 20 min → 5 min target

### Q2 Debt Work

- Database index analysis (missing indexes slowing queries)
- API versioning (cleanup deprecated v1 endpoints)
- Documentation refresh (onboarding takes too long)

### Q3-Q4 Debt Work

- Schema migration (legacy user table fields causing N+1 queries)
- Monitoring debt (dashboards unmaintained; alerts too noisy)

**Success criteria**: By end of Q4, deploy time <5 min, test pass rate >98%, library vulnerability count <10

---

## What We're NOT Doing (and Why)

- **API rate limiting**: Low customer demand; competitive advantage is features, not APIs. Revisit 2027 if needed.
- **Multi-region deployment**: Business prioritizes single-region until 2025. Infrastructure cost/complexity too high for 15% revenue growth. 2027 objective.
- **Blockchain settlement**: Interesting but premature. No customer asks. Market still immature. Monitor 2027.
- **Mobile app**: Native iOS/Android not a customer request. Web + mobile browser sufficient. Revisit if mobile usage >40%.
- **Event sourcing migration**: Current event model works. Migration complex + risky. Audit trails can be solved with current DB.

---

## Risk & Mitigations

| Risk                                              | Likelihood | Impact                                | Mitigation                                                          |
| ------------------------------------------------- | ---------- | ------------------------------------- | ------------------------------------------------------------------- |
| APM vendor onboarding takes >4 weeks              | Medium     | Delays incident response improvements | Start vendor evaluation in December; have backup vendor             |
| Database sharding more complex than estimated     | Medium     | Spills into Q4, blocks 2027 roadmap   | POC in Q3 validates complexity; adjust Q4 timeline if needed        |
| KYC third-party integration has compliance issues | Low        | Audit delay, revenue hold             | Engage compliance partner in Q1; pre-audit integration              |
| PCI-DSS v4 findings require emergency fixes       | Low        | Mid-Q2 firefighting                   | Hire external auditor in Q1 for pre-audit assessment                |
| Team attrition (burnout from on-call)             | Medium     | Loses context, slows delivery         | Incident response program improves on-call; hire +2 engineers in Q2 |
| Scope creep (new product features added)          | High       | Roadmap overload                      | Lock Q1-Q2 capacity; new features queue for Q3-Q4                   |

---

## Hiring Assumptions

- **Current team**: 18 engineers (6 senior, 8 mid, 4 junior)
- **Projected additions**: +2 senior engineers by Q2 (hire in Q1)
- **Impact on roadmap**: Without new hires, Scale theme slides to Q4 (revisit in Jan if hiring blocked)

If hiring plan changes, we'll reprioritize: defer Scale to 2027, focus Q2-Q3 on Reliability + Compliance only.

---

## Success Metrics

| Metric                        | Current     | Target (End of 2026) | Why This Matters                               |
| ----------------------------- | ----------- | -------------------- | ---------------------------------------------- |
| MTTD (Mean Time to Detect)    | 30 min      | 10 min               | Faster incident response; less customer impact |
| MTTR (Mean Time to Recover)   | 2 hours     | 30 min               | Reduces downtime revenue loss                  |
| Database query latency        | 200ms       | 50ms                 | Faster transactions; better UX                 |
| Database capacity utilization | 85%         | 40%                  | Room for 10x growth without overhaul           |
| On-call pages/week            | 15          | 8                    | Team burnout reduction; retention improvement  |
| PCI-DSS certification         | Not audited | Certified            | Required for enterprise customers              |
| Test pass rate                | 92%         | 98%                  | More reliable CI/CD; faster merges             |
| Deploy time                   | 20 min      | 5 min                | Product velocity 4x improvement                |

---

## Reassessment Gates

**Conditions that would trigger roadmap changes:**

- **Major competitor launches feature**: If Stripe/PayPal ship feature we promised, prioritize immediately
- **High-value customer churn**: If customer >$100K/year churns due to technical limitation, escalate
- **Team attrition**: Engineer leaves; reallocate capacity; adjust roadmap
- **Regulatory change**: New compliance requirement (GDPR-style); shift Compliance capacity
- **Infrastructure emergency**: Sustained outages; pause features, focus on stability

**Formal review**: End of each quarter (Jan 31, Apr 30, Jul 31, Oct 31)

---

## Alternatives Considered & Trade-Offs

### Alternative 1: Skip Reliability, Focus on Compliance + Scale (Rejected)

**Why rejected**: On-call burnout is a real risk; team is stretched. Incident response takes 3-4 people; scaling without observability leads to more incidents, not fewer. Better to fix reliability first.

### Alternative 2: Multi-region in 2026 instead of 2027 (Rejected)

**Why rejected**: Cost-benefit unfavorable. Would consume 40% of capacity; current single-region sufficient. 2027 is better timing when we have more stable infrastructure and team.

### Alternative 3: Outsource KYC instead of building (Evaluated but rejected)

**Why rejected**: Vendor lock-in risk; compliance audit trail important. Building in-house gives us control. Plus, +$100K MRR justifies engineering investment.

---

## Document Metadata

| Property         | Value                                     |
| ---------------- | ----------------------------------------- |
| Owner            | VP Engineering (Michael Lee)              |
| Created          | 2025-12-01                                |
| Last Updated     | 2026-01-15                                |
| Review Frequency | Quarterly (end of each quarter)           |
| Stakeholders     | Exec team, board, product, finance, sales |
| Next Review      | 2026-03-31 (end of Q1)                    |

---

## Sign-Off

- [ ] **VP Engineering approval**: Michael Lee ********\_******** Date: ****\_****
- [ ] **Product Lead approval**: Sarah Wong ********\_******** Date: ****\_****
- [ ] **CFO approval** (budget alignment): Bob Chen ********\_******** Date: ****\_****

---

## Q1 Execution Plan (January - March)

**Week 1-2**: APM vendor selection & onboarding start
**Week 3-4**: Logging standardization across services
**Week 5-8**: APM deployment + incident response program
**Week 9-12**: Elasticsearch → OpenSearch migration
**Week 11-12**: Q2 planning & KYC vendor selection
**Buffer**: 2-3 weeks for production issues/optimizations

**Success criteria for Q1**: APM operational, <10 min MTTD validated, incidents documented in runbooks
