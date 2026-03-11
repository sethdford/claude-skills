# Example: RICE Scoring for Analytics Platform

## Context

**Company**: Analytics SaaS platform for ecommerce brands

**Sizing**: 5,000+ customers, $2M ARR, 18-person engineering team

**Scenario**: Q2 planning. Product team has 6 competing opportunities. Engineering has capacity for ~3 major initiatives this quarter.

---

## Scoring Framework

**RICE Parameters Used**:

- **Reach**: Estimated number of customers affected in 3 months
- **Impact**: How much better are their lives? (3x = 3x revenue/engagement per user, 2x = 2x, etc.)
- **Confidence**: How sure are we about this scoring? (100% = proven market demand, 50% = educated guess, 25% = still researching)
- **Effort**: Engineering time in weeks

---

## Opportunities Scored

### Opportunity 1: Real-Time Dashboard Updates

**Description**: Stream data to dashboard instead of 30-second polling intervals. Customers see metrics update live.

**Scoring**:

- **Reach**: 3,200 customers (power users who use dashboard daily)
- **Impact**: 2x (better UX; customers say it would save 2 min/day in monitoring)
- **Confidence**: 90% (100+ customer interviews confirmed this)
- **Effort**: 6 weeks (WebSocket server, frontend realtime, subscription tier logic)

**RICE Score**: (3,200 × 2 × 0.90) / 6 = **960**

**Notes**: High reach, proven demand, realistic scope

---

### Opportunity 2: Custom Event Tracking

**Description**: Let customers define custom events (not just pageviews). More flexible analytics.

**Scoring**:

- **Reach**: 1,500 customers (mostly enterprise accounts; SMBs don't ask)
- **Impact**: 3x (enterprise customers say this would block 3-4 custom integrations)
- **Confidence**: 70% (strong from enterprise cohort; weaker from SMB)
- **Effort**: 10 weeks (event schema, validation, ingestion pipeline, UI builder)

**RICE Score**: (1,500 × 3 × 0.70) / 10 = **315**

**Notes**: High impact but lower reach and confidence; complex engineering

---

### Opportunity 3: Embedded Dashboards (White-Label)

**Description**: Customers can embed analytics dashboards in their product (white-labeled). New revenue stream.

**Scoring**:

- **Reach**: 800 customers (mostly enterprise)
- **Impact**: 2x (enterprise sees this as strategic; would increase retention and NRR)
- **Confidence**: 50% (some interest; not proven demand yet)
- **Effort**: 12 weeks (embedding SDK, authentication, usage metering, billing integration)

**RICE Score**: (800 × 2 × 0.50) / 12 = **67**

**Notes**: Strategic but unproven; highest effort; lowest confidence

---

### Opportunity 4: Export to Data Warehouse

**Description**: Customers can export raw events to their data warehouse (BigQuery, Redshift, Snowflake). Data access + integration revenue.

**Scoring**:

- **Reach**: 2,200 customers (enterprise + power users)
- **Impact**: 2x (removes dependency on third-party tools; reduces churn)
- **Confidence**: 85% (strong enterprise demand; positive reviews about this in NPS comments)
- **Effort**: 5 weeks (batch job scheduler, schema mapper, connector to 3 warehouses, SDK update)

**RICE Score**: (2,200 × 2 × 0.85) / 5 = **748**

**Notes**: High reach, strong signal, reasonable effort

---

### Opportunity 5: Mobile App (Native)

**Description**: iOS/Android native app for viewing dashboards on mobile.

**Scoring**:

- **Reach**: 3,500 customers (everyone using dashboards)
- **Impact**: 1.5x (nice to have; not core to workflow; some people check dashboards on mobile 1-2x/week)
- **Confidence**: 60% (lukewarm in surveys; "would be nice")
- **Effort**: 14 weeks (iOS dev, Android dev, sync state, offline support)

**RICE Score**: (3,500 × 1.5 × 0.60) / 14 = **225**

**Notes**: Highest reach but low impact and confidence; massive effort

---

### Opportunity 6: Performance Improvements (Slow Queries)

**Description**: Query engine optimization. Currently slow for customers with 1M+ events/day.

**Scoring**:

- **Reach**: 150 customers (top tier, heavy volume)
- **Impact**: 3x (saves them $50K/year in compute; huge churn risk if we don't fix)
- **Confidence**: 95% (we have data; queries are objectively slow)
- **Effort**: 8 weeks (query planner rewrite, indexing strategy, load testing)

**RICE Score**: (150 × 3 × 0.95) / 8 = **54**

**Notes**: Highest impact, high confidence, but low reach (niche problem)

---

## Results & Planning Summary

### Rank by RICE Score

| Rank | Opportunity                 | RICE Score | Recommendation                                                |
| ---- | --------------------------- | ---------- | ------------------------------------------------------------- |
| 1    | Real-Time Dashboard Updates | 960        | **COMMITTED** — Q2                                            |
| 2    | Export to Data Warehouse    | 748        | **COMMITTED** — Q2                                            |
| 3    | Custom Event Tracking       | 315        | **PURSUING IF CAPACITY** — Q3 if team ahead of schedule       |
| 4    | Mobile App                  | 225        | **BACKLOG** — Revisit Q4 when team grows                      |
| 5    | Embedded Dashboards         | 67         | **RESEARCH/VALIDATE** — Survey enterprise; de-risk confidence |
| 6    | Performance Improvements    | 54         | **COMMITTED** — Q2 (technical necessity despite low RICE)     |

### Planning Decisions

**Committed for Q2** (70% capacity):

- Real-Time Dashboard Updates (6 weeks)
- Export to Data Warehouse (5 weeks)
- Performance Improvements (8 weeks) — _[Technical debt; protects churn risk]_

**Pursuing if Capacity** (20% capacity):

- Custom Event Tracking — If team ships committed items 1-2 weeks early

**Research/Validate** (10% capacity):

- Embedded Dashboards — Run enterprise survey; build lightweight POC; gauge demand

**Backlog** (revisit Q3-Q4):

- Mobile App — Defer until after Q2 growth initiatives; revisit with native mobile team

### Key Insights

1. **Real-Time Updates** is the clear winner: proven demand, high reach, realistic scope.
2. **Data Warehouse Export** is a strong second: opens new revenue channel, high enterprise interest.
3. **Custom Events** is interesting but risky: high impact but only for 30% of customer base; worth validating demand further before committing.
4. **Mobile App** is a vanity feature: high reach but low impact; customers rarely request it; massive effort relative to value.
5. **Performance tuning** isn't scoring well by RICE, but it's a business necessity for our top customers; we commit to it anyway as a hedge against churn.

### Q2 Capacity Allocation

- **Committed initiatives**: ~19 weeks (out of ~18-week quarter) — tight but doable with focused team
- **Risk mitigation**: If Real-Time Updates overruns, we defer Custom Events validation or reduce Export scope
- **Buffer**: Embedded Dashboards research as "nice to have" if team moves fast

---

## Review & Decisions

**Scoring Review Date**: 2026-02-15

**Reviewed by**: [PM Lead], [Eng Lead], [Customer Success Lead]

**Notes**:

- Enterprise customers validated Data Warehouse need (5 customer calls)
- Real-Time Updates emerged from NPS open-ended feedback (23 mentions in last 100 responses)
- Performance improvements are a hedge against churn in top 150 accounts
- Mobile App deferred; revisit when iOS/Android demand reaches 70%+ in surveys

**Next Steps**:

1. Kick off Real-Time Updates and Export to Data Warehouse (start next week)
2. Run Enterprise survey on Embedded Dashboards (complete by end of Feb)
3. Schedule performance tuning work for mid-Q2 (after Data Warehouse ships)
