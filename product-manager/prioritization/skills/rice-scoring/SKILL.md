---
name: rice-scoring
description: Quantify and rank opportunities using the RICE framework (Reach, Impact, Confidence, Effort) to enable data-driven prioritization and trade-off discussions. Use when comparing diverse features, deciding what to build next, or allocating engineering time across initiatives.
allowed-tools: Read, Grep, Glob, Write, Edit
---

# RICE Scoring: Quantitative Opportunity Prioritization

Rank a backlog of opportunities using RICE (Reach, Impact, Confidence, Effort) to remove bias and enable transparent trade-off conversations across product, design, and engineering.

## Context

You are helping a product team prioritize what to build next. A backlog typically contains 30-100+ ideas; without a systematic framework, prioritization devolves into politics (whoever speaks loudest wins) or guesswork. RICE provides a transparent, quantifiable scoring system that makes trade-offs visible and defensible.

RICE is not magic; it's a tool for organizing thinking. The value comes from the _estimation process_—asking "who will this affect?" and "how confident are we?"—not from the final score. Use RICE to start conversations, not to end them.

## Domain Context

- **Sean McBride's RICE Framework** (Intercom): Reach × Impact × Confidence / Effort. Designed specifically for product teams making prioritization decisions.
- **Reach**: How many users/customers will this affect? (absolute number or segment size)
- **Impact**: How much value per affected user? (massive=3, high=2, medium=1, low=0.5)
- **Confidence**: How confident are we in these estimates? (as a percentage: 100%, 75%, 50%, 25%)
- **Effort**: Engineering effort in person-months or points (not complexity, not risk—just engineering labor)
- **The Formula**: (Reach × Impact × Confidence) / Effort = RICE score
- **High-effort, high-impact work** should bubble up; low-reach, high-effort work should drop
- **Confidence matters**: A half-baked estimate (50% confidence) reduces the score proportionally, which is correct
- **Calibration is key**: Estimation consistency matters more than absolute accuracy; teams should calibrate together

## When to Use This Skill

- You have a backlog of 20+ feature ideas and need to decide which 3-5 to work on next
- You're allocating engineering resources across multiple product areas (which team gets the engineer?)
- You need to defend your prioritization to stakeholders ("Why this instead of that?")
- Leadership is pushing for Feature X; you need to show quantitatively why Feature Y scores higher
- You're planning Q1/Q2 roadmap and want transparent trade-offs
- You want to resurface old ideas that may now have higher priority (RICE can shift as context changes)

## Prerequisites

Before starting RICE scoring, gather:

1. **Candidate opportunities**: A list of 20-100 feature ideas, improvements, bugs, or technical debt items
2. **Data**: User segment sizes, usage metrics, churn rates, customer feedback, support load
3. **Engineering input**: Rough effort estimates for each opportunity (in points or person-months)
4. **Customer evidence**: Which opportunities are validated vs. speculative
5. **Business context**: Are there strategic priorities, commitments, or constraints?

If you're missing data, estimate based on best judgment and note the confidence. Don't wait for perfect data.

## Instructions

### 1. List All Opportunities

Write down every candidate opportunity: features, improvements, bug fixes, infrastructure improvements, experiments. Don't filter yet. Aim for 20-50 items.

Example:

- Add dark mode toggle
- Fix issue where users' profiles fail to load on slow networks
- Build Slack integration
- Improve onboarding flow (30-min task is confusing users)
- Add export-to-PDF for reports
- Migrate to new database (infrastructure)
- Build API for third-party developers

### 2. Define Scoring Parameters (Team Calibration)

Before scoring, align the team on what each dimension means:

**Reach**:

- Measured in: number of users per quarter, or % of user base
- Example: "10,000 users per quarter" or "25% of user base"
- Note: Reach should be the # of users _affected by the change_, not total users

**Impact** (value per affected user):

- **Massive** (3x): Dramatically changes how users accomplish their goal (e.g., a 5x speedup, or removes a critical blocker)
- **High** (2x): Meaningful improvement; users will notice (e.g., 50% faster, solves major friction)
- **Medium** (1x): Visible improvement; nice-to-have (e.g., new feature, modest speedup)
- **Low** (0.5x): Minor improvement; users might not notice (e.g., UI polish, very small perf gain)

**Confidence** (% estimate accuracy):

- **100%**: We have direct data (e.g., we measured it, customers asked for it, we've shipped similar before)
- **75%**: Good data, some uncertainty (e.g., user interview signals, analytics tell us most of the story)
- **50%**: Educated guess (e.g., we think this will help, but haven't validated)
- **25%**: Speculative (e.g., we think this might help, but very uncertain)
- Don't use confidences below 25%; if you're that uncertain, do research first

**Effort** (engineering labor):

- Measured in: person-months, engineer-weeks, story points (pick one, be consistent)
- Example: "2 people × 2 weeks = 4 engineer-weeks" or "3 story points"
- Important: Effort ≠ complexity. A complex feature might take 2 weeks if 5 engineers work on it in parallel. Effort is calendar time.
- Include design, QA, deployment; not just coding

### 3. Score Each Opportunity

For each candidate, estimate Reach, Impact, Confidence, and Effort.

| Opportunity          | Reach | Impact | Confidence | Effort (weeks) | RICE Score                     |
| -------------------- | ----- | ------ | ---------- | -------------- | ------------------------------ |
| Add dark mode        | 8,000 | 0.5    | 75%        | 2              | (8000 × 0.5 × 0.75) / 2 = 1500 |
| Fix profile load bug | 2,000 | 2      | 100%       | 1              | (2000 × 2 × 1.0) / 1 = 4000    |
| Slack integration    | 1,500 | 3      | 50%        | 6              | (1500 × 3 × 0.5) / 6 = 375     |
| Improve onboarding   | 3,000 | 2      | 75%        | 4              | (3000 × 2 × 0.75) / 4 = 1125   |

### 4. Identify Scoring Patterns

Look for:

- **High-reach, low-effort wins**: Small investment, big payoff (prioritize these)
- **High-impact, low-confidence items**: Worth validating through research before prioritizing
- **Low-reach, high-effort items**: Red flag—question whether this is worth doing
- **High-reach, high-effort items**: Strategic bets; usually worth doing, but plan them carefully
- **Strategic initiatives** (infrastructure, platform improvements): Often lower reach/impact but necessary for business health

### 5. Rank & Review

Sort by RICE score (highest first). Then review with team:

1. Does the ranking make intuitive sense?
2. Are there business/strategic reasons to override the score? (e.g., committed customer, strategic tie-in)
3. Are there dependencies? (Feature A must ship before Feature B)
4. Are estimates realistic? (Can engineering actually do 4 weeks of work in this 4-week sprint, or is there context switching?)

### 6. Plan Roadmap

Select top opportunities to fill your next roadmap period (next quarter or 6 weeks). Typically:

- 60-70% on highest-scoring opportunities
- 20-30% on medium-scoring work (technical debt, infrastructure)
- 10% on experiments or lower-scoring but strategic initiatives

## Output Format

A RICE scoring spreadsheet (shared with team) + a 1-page summary:

```
# Q2 2024 Opportunity Prioritization (RICE Scoring)

## Top Opportunities (Next Quarter)

| Rank | Opportunity | Reach | Impact | Confidence | Effort | RICE | Notes |
|------|-------------|-------|--------|------------|--------|------|-------|
| 1 | Fix profile load bug | 2,000 | 2x | 100% | 1 week | 4,000 | Critical path blocker; high ROI |
| 2 | Improve onboarding flow | 3,000 | 2x | 75% | 4 weeks | 1,125 | Affects trial-to-paid conversion |
| 3 | Add dark mode | 8,000 | 0.5x | 75% | 2 weeks | 1,500 | User-requested; modest impact |
| 4 | Build Slack integration | 1,500 | 3x | 50% | 6 weeks | 375 | High impact IF we ship, but uncertain |

## Summary

**Plan**: Commit to #1-3 for Q2 (6 weeks engineering). #4 is lower priority unless customer commits or we validate demand.

**Rationale**: #1-2 have highest RICE scores and will improve core metrics. #3 is user-requested and has good reach. #4 is speculative; recommend research spike before committing engineering.

**Confidence**: High on #1-2 (backed by data). Medium on #3 (user requests, but impact is modest). Low on #4 (speculative; needs customer validation).
```

## Worked Example

**Q2 2024 Opportunity Prioritization: Analytics Platform**

| Rank | Opportunity                     | Reach  | Impact | Confidence | Effort (weeks) | RICE Score | Notes                                             |
| ---- | ------------------------------- | ------ | ------ | ---------- | -------------- | ---------- | ------------------------------------------------- |
| 1    | Fix funnel abandonment bug (P1) | 5,000  | 2x     | 100%       | 1              | 10,000     | ~100 customers affected; blocks critical workflow |
| 2    | Segment users by cohort         | 4,000  | 2x     | 75%        | 3              | 2,000      | Top customer request; impacts key use case        |
| 3    | Add real-time alerts            | 2,000  | 3x     | 50%        | 8              | 375        | High impact but effort-heavy; lower confidence    |
| 4    | Dark mode                       | 8,000  | 0.5x   | 75%        | 2              | 1,500      | User-requested; low impact                        |
| 5    | Build API                       | 500    | 3x     | 25%        | 6              | 62         | Could unlock integrations; very uncertain         |
| 6    | Improve page load (3s → 1s)     | 12,000 | 1x     | 100%       | 4              | 3,000      | Affects all users; good ROI                       |

**Decision**:

- **Ship in Q2**: #1, #2, #6 (6 weeks effort, high RICE scores, solid confidence)
- **Research/validate**: #3, #5 (speculative; do customer interviews before committing)
- **Backlog**: #4 (nice-to-have, can ship if we finish early)

---

## Decision Framework

When estimating and facing uncertainty:

- **If you don't know Reach**: Ask "How many customers/users have this problem?" If <100, Reach is low. If >10K, Reach is high.
- **If you don't know Impact**: Ask "Would this change how users accomplish their goal?" or "Would users pay extra for this?" If yes → high. If no → low.
- **If Impact feels subjective**: Compare against a known baseline (e.g., "Is this as valuable as Feature X that we shipped last quarter?")
- **If Confidence is low**: Recommend a research spike before prioritizing (e.g., "Do 5 customer interviews to validate demand")
- **If Effort is uncertain**: Ask engineering for a wide range ("2-4 weeks?") and use the midpoint. Note the uncertainty.
- **If an opportunity has zero Reach**: Don't score it; it's not a customer problem (might be technical debt, which should be scored separately under infrastructure)

## Anti-Patterns & Guards

### Anti-Pattern 1: Reach Inflation

**Description**: Claiming "all 100,000 users" will be affected by a feature, when really only power users (10% = 10,000) will use it.

**Why LLMs make this mistake**: Maximizing Reach makes the RICE score higher, so LLMs unconsciously inflate it.

**Guard**: Always ask "Will _this specific user segment_ use this feature?" Don't count users who won't notice the change.

**Example**:

- ❌ Bad: Dark mode affects "all 100,000 users"
- ✓ Good: Dark mode affects "users who keep the app open for 2+ hours/day" = ~30% = 30,000 users

### Anti-Pattern 2: Impact Confusion

**Description**: Confusing the _importance_ of a problem with the _impact_ of a solution. High-reach + low-impact = high RICE score, but building it is wrong.

**Why LLMs make this mistake**: LLMs see "important customer problem" and score impact as high, without thinking about the solution's magnitude.

**Guard**: Ask "If we ship this, how much better will users' lives be?" A dark mode is nice, but it doesn't change productivity (low impact). Reducing onboarding time from 2 hours to 30 minutes _does_ change productivity (high impact).

**Example**:

- ❌ Bad: "Onboarding is a problem (high importance) → Dark mode solves it (impact = 2x)" [doesn't make sense]
- ✓ Good: "Onboarding is a problem. Simplifying it from 2 hours to 30 min is high impact (2x). Dark mode is unrelated to onboarding."

### Anti-Pattern 3: Over-Confidence

**Description**: Using 100% confidence on speculative features ("We built something similar once, so we know how to do this").

**Why LLMs make this mistake**: LLMs assume past success = future success; they don't account for unique project risks.

**Guard**: Reserve 100% confidence for items you've already measured or shipped. For new opportunities, start at 50% or 75% unless you have strong validation.

### Anti-Pattern 4: Effort Underestimation

**Description**: Underestimating engineering effort ("It's just a UI tweak"), leading to inflated RICE scores and missed timelines.

**Why LLMs make this mistake**: LLMs don't account for testing, edge cases, or context-switching overhead.

**Guard**: Always involve engineering in effort estimation. Include design, QA, and deployment. If uncertain, add 50% buffer.

### Anti-Pattern 5: Not Revising Scores as Context Changes

**Description**: Scoring opportunities once, then never revisiting. But priorities shift (new customer, market change, data).

**Why this fails**: RICE is static; real business is dynamic.

**Guard**: Re-score backlog quarterly or when major context shifts (big customer, strategic pivot).

## Quality Checklist

Before sharing RICE scores:

- [ ] **Reach is grounded**: Based on user segment size, not gut feel; accounts for adoption rate if applicable
- [ ] **Impact reflects the solution, not the problem**: Don't confuse importance with magnitude
- [ ] **Confidence is calibrated**: Team agrees on what 75% vs. 50% means; used consistently
- [ ] **Effort includes all work**: Design, engineering, QA, deployment; not just coding
- [ ] **Outliers explained**: High-RICE-score items make intuitive sense; low-score items have clear rationale
- [ ] **Dependencies noted**: If Feature A blocks Feature B, that's explicit
- [ ] **Business context visible**: Strategic priorities or constraints are noted
- [ ] **Team reviewed**: Engineering, design, and product agree on estimates (or disagreement is noted)

## Further Reading

- McBride, Sean. "Intercom on Product: How to Prioritize Features" (Intercom Blog). Introduces RICE framework.
- Cagan, Marty. _Inspired: How to Create Products Customers Love_. Wiley, 2008. Chapters on prioritization frameworks.
- Olsen, Dan. _The Lean Product Playbook_. Wiley, 2015. On running prioritization exercises.
- Patton, Jeff. _Dual Track Agile_ (presentation). On splitting discovery from delivery; helps calibrate Confidence in RICE.
- Gothelf, Jeff and Josh Seiden. _Lean UX_. O'Reilly, 2013. On iterative prioritization and learning.
