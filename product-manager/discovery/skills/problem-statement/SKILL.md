---
name: problem-statement
description: Define a clear, evidence-based problem statement that frames customer pain without prescribing solutions. Use when discovering unmet customer needs, validating market problems, or prioritizing discovery research.
allowed-tools: Read, Grep, Glob, Write, Edit
---

# Problem Statement

Create a focused, evidence-based problem statement that isolates customer pain, quantifies its impact, and avoids solution bias before ideating or building.

## Context

You are a senior product manager conducting problem discovery for a customer segment or market. Your role is to gather direct evidence of customer struggle, understand the context in which it occurs, and articulate the problem in language that resonates with both the customer and the team.

Problem discovery is foundational work—it prevents the organization from building the wrong solution. A well-framed problem statement becomes the north star for downstream design, engineering, and go-to-market decisions. Weak problem statements lead to misaligned teams, wasted engineering effort, and products that don't resonate with customers.

## Domain Context

- **Teresa Torres' Continuous Discovery**: Emphasizes observable customer behaviors over assumed problems; problems emerge from recurring friction, not intuition
- **Jobs-to-be-Done (Christensen)**: Separates the job (what the customer is trying to accomplish), the context (circumstances), and the friction (obstacles preventing successful job completion)
- **Clayton Christensen's "Competing Against Luck"**: Wealthy companies often miss problems because they listen to successful customers, not struggling ones
- **Problem vs. Symptom**: A symptom is "users are churning"; the problem is "users churn because first-time value isn't clear and onboarding takes 4 hours"
- **Evidence Hierarchy**: Direct customer quotes > Behavioral data (session recordings, heatmaps) > Survey data (self-reported) > Assumptions or internal intuition
- **Problem Validation**: Before solving, confirm the problem is: real (customers describe it), frequent (happens regularly), and impactful (customers care enough to change behavior)

## When to Use This Skill

- You've noticed a pattern of customer struggle in interviews, support tickets, or usage data and want to articulate it clearly
- You're evaluating whether a customer problem is worth solving (before design or engineering effort)
- Your team is misaligned on what problem you're solving; you need a north star
- A customer segment is underperforming, and you want to diagnose why before proposing solutions
- You're building a discovery roadmap and need to scope which problems to research first

## Prerequisites

Before using this skill, gather:

1. **Customer interviews or user research**: 5+ direct conversations with customers experiencing the problem (not executives or successful power users)
2. **Behavioral data**: Session recordings, support ticket trends, feature usage patterns, churn data
3. **Quantitative signals**: How many customers affected? How often does it occur? What's the business impact (revenue, churn, support cost)?
4. **Segment clarity**: Which customer segment experiences this problem most acutely? (Geography, company size, industry, use case)
5. **Context**: When, where, and with whom does this problem emerge? What are customers trying to accomplish when it happens?

If you're starting from zero research, spend time gathering this evidence first before writing the problem statement.

## Instructions

### 1. Gather and Synthesize Evidence

- **Customer interviews**: Conduct 5-8 interviews with customers currently struggling with this problem. Listen for unprompted mentions of friction, workarounds, frustration.
- **Extract direct quotes**: Capture 3-5 quotes where customers describe the problem in their own words. These are gold.
- **Behavioral signals**: If available, pull session recordings showing the struggle (e.g., user abandoning onboarding, repeatedly clicking a non-functional feature, support chat escalations)
- **Quantify**: What % of your user base hits this problem? How frequently per week/month? What's the revenue or churn impact?

### 2. Identify the Core Friction (Not the Symptom)

- Ask yourself: "What's the job the customer is trying to do?" (e.g., "I'm trying to set up my team's Slack integration in under 5 minutes")
- Ask: "What's stopping them?" (e.g., "The setup requires 3 different services; I don't know which order to configure them")
- Avoid: "Our integration flow is confusing." Instead: "Product managers want to integrate Slack with their CRM but don't understand the prerequisite dependencies; they abandon setup after 2 steps."

### 3. Define the Customer Segment Precisely

- **Not**: "All users struggle with this"
- **Instead**: "B2B SaaS product managers with <5-person teams, setting up their first CRM integration, without technical support from IT"
- Be specific about: company size, role, experience level, use case, timeline, industry if relevant

### 4. Quantify Impact (Business + Emotional)

- **Quantitative**: "25% of free trial users abandon onboarding after step 2; step 2 takes 18 minutes average. We lose $40K ARR annually from this cohort."
- **Qualitative**: "Customers express frustration; support sees 5+ tickets/week from users stuck at the same step."
- **Outcome impact**: "If we solve this, we expect churn to drop 15% in this cohort; +$120K ARR annually."

### 5. Write the Problem Statement

Use this template, then adapt to your language:

> **Problem Statement: [Feature/Domain]**
>
> **Segment**: [Specific customer group]
>
> **Problem**: [Customer's own words describing the friction]
>
> **Context**: [When/where does this occur? What are they trying to accomplish?]
>
> **Impact**: [How many? How often? Business consequence?]
>
> **Evidence**: [3-5 customer quotes, behavioral data, metrics]

Example (realistic, not generic):

> **Problem Statement: Onboarding Abandonment for B2B SaaS Product Teams**
>
> **Segment**: Mid-market B2B SaaS PMs (10-50 employees) setting up their first Zapier integration, without an engineering hire yet.
>
> **Problem**: "I don't know what order to connect these apps. The docs assume I'm a developer. After 15 minutes, I give up and do it manually." — User research, Week 3 post-signup
>
> **Context**: A product manager just signed up; they're motivated to automate sales data syncs. They open the integration docs expecting a step-by-step wizard but see API references instead. They try trial-and-error but hit configuration errors. By step 3, they abandon setup and manually export/import data weekly (taking 30 min/week).
>
> **Impact**: 28% of free trial users hit this flow; 23% abandon post-trial conversion. Estimated $60K annual ARR lost from this cohort. Support team spends 4 hours/week explaining integration sequencing.
>
> **Evidence**:
>
> - Session recordings: 6/8 users tested hit the config error (avg 18 min before abandonment)
> - Direct quote from trial user: "I expected a wizard, not an API reference"
> - Support ticket trends: 5-7 tickets/week from users asking "What's the right order to connect these?"
> - Segment churn: Users who complete onboarding convert at 32%; users who abandon at step 2 convert at 2%

### 6. Stress-Test Your Problem Statement

Ask yourself:

- **Is this observable?** Can you point to a customer exhibit (quote, session recording, support ticket) that proves this problem exists? Or did we infer it?
- **Is it frequent?** Does this happen regularly, or was it one customer's edge case?
- **Does the customer care?** Would they change behavior or pay to solve this? (If they tolerate it indefinitely, it's not a problem worth solving.)
- **Is it the real problem?** Or is it a symptom? (Ask "why" 5 times to dig to root cause.)

## Output Format

A 1-2 page problem statement document (sharable with engineering, design, stakeholders):

```
# Problem Statement: [Name]

## Customer Segment
[Specific group, with relevant context]

## Problem
[In customer's language, not company language]

## Context
[When/where/why does this occur?]

## Impact
[Quantified: how many, how often, business consequence]

## Evidence
- Direct customer quotes (3-5, from interviews/support)
- Behavioral data (session recordings, feature usage, churn patterns)
- Quantitative metrics (segment size, problem frequency, conversion impact)

## Validation Status
[ ] Real (confirmed via customer interview)
[ ] Frequent (occurs regularly, not one-off)
[ ] Impactful (customer would change behavior to solve; business case exists)

## Next Steps
- [ ] Share with engineering to understand technical constraints
- [ ] Share with design to brainstorm solutions
- [ ] Plan discovery research to validate potential solutions
```

## Worked Example

**Problem Statement: Small SaaS Teams Can't Understand Complex Funnel Drop-Off**

**Segment**: B2B SaaS product teams (5-20 people), no dedicated analytics hire, using our product to run growth experiments.

**Problem**: "I see users dropping off at step 3 of our funnel, but your tool doesn't explain why. I have to export the data and build a custom pivot table in Excel to understand what's happening. That takes 2 hours, and by then I'm weeks behind on my hypothesis."

**Context**: A PM just launched a new feature and wants to track adoption. They create a funnel in our product. The funnel shows drop-off but no segmentation; they can't see if the problem is mobile vs. desktop, or if certain user cohorts convert better. They want to dig deeper but lack the technical skills to write SQL. They give up and revert to manual Excel analysis.

**Impact**:

- 32% of trial users create a funnel but don't progress to paid activation (estimated $45K ARR lost annually from this cohort)
- Support team spends 3 hours/week explaining why drop-off is happening for specific segments
- Churn in this segment is 18% post-trial vs. 8% for power users who write SQL

**Evidence**:

- Session recordings: 5/7 trial users abandon after viewing a funnel with >15% drop-off
- Support tickets: "How do I see drop-off by device type?" (8 tickets/month for 6 months)
- Customer quote: "I don't know SQL, so I can't slice the data the way I want. I'll just stick with Google Analytics."
- Usage data: Trial users who create funnels convert at 5%; those who don't create funnels convert at 28% (selection effect: power users converge more)

---

## Decision Framework

When you face ambiguity during problem discovery:

- **If interview mentions a problem once, ask**: "Is this a pattern or an edge case?" Dig for frequency by asking, "Does this happen regularly?" or "How often do you encounter this?"
- **If you see a workaround (e.g., manual Excel export)**: This is a strong signal of an unmet need. Ask why they're not using the tool instead.
- **If the problem is vague (e.g., "our onboarding is confusing")**: Ask "What specifically is confusing?" Get concrete. "Step 2 asks me to configure X, but I don't know what X is" is concrete.
- **If the customer is successful despite the problem**: Question whether it's worth solving. If the pain isn't severe enough to change behavior, it's not a "problem" yet—it's a "nice-to-have."
- **If you're inferring the problem vs. hearing it directly**: Pause. Go back to customers. Don't solve imagined problems.

## Anti-Patterns & Guards

### Anti-Pattern 1: Solution Bias

**Description**: Writing "We need a mobile app for real-time notifications" instead of "Users miss time-sensitive updates while away from their desk."

**Why LLMs make this mistake**: LLMs are trained on solution-forward language (feature specs, product briefs). Problem statements require customer empathy, not feature ideation.

**Guard**: If your problem statement mentions a specific technology, feature, or solution, rewrite it from the customer's perspective. Remove all solution language.

**Example**:

- ❌ Bad: "We need to simplify the integration setup with a wizard UI"
- ✓ Good: "Product teams setting up integrations for the first time don't understand the prerequisite configuration steps and abandon after 15 minutes"

### Anti-Pattern 2: Confusing Symptom with Root Cause

**Description**: "Users are churning" vs. "Users churn because onboarding takes 4 hours and first-use value isn't clear."

**Why LLMs make this mistake**: LLMs often stop at the surface observation and don't dig deeper into causation.

**Guard**: Apply the "5 Whys" framework. For each problem statement, ask "Why?" 5 times and see if you reach the real root cause.

**Example**:

1. Why: Users are churning → Because they don't see value early
2. Why: They don't see value early → Because onboarding is long
3. Why: Onboarding is long → Because it requires 3 manual steps
4. Why: It requires manual steps → Because our API doesn't auto-detect user data
5. Why: Our API can't auto-detect → [Technical root cause]

### Anti-Pattern 3: Assuming the Problem Without Customer Evidence

**Description**: Claiming a problem is urgent without interviews, support data, or usage patterns to back it up.

**Why LLMs make this mistake**: LLMs can generate plausible-sounding problems based on logical inference, not ground truth.

**Guard**: For every problem statement, cite the source: direct quote from interview, support ticket trend, session recording, churn cohort analysis. If you can't cite it, keep researching.

### Anti-Pattern 4: Writing for a Segment That's Too Broad

**Description**: "All users struggle with this" instead of "B2B SaaS PMs with <5-person teams, in year 1 of their product."

**Why LLMs make this mistake**: Generalization feels safer and more universally applicable. But broad segments dilute focus and lead to mediocre solutions.

**Guard**: Segment ruthlessly. Include: industry (B2B SaaS vs. B2C vs. Enterprise), company size (early-stage vs. mid-market), role, experience level, use case, timeline. If your segment description doesn't fit on one line, you're being too broad.

### Anti-Pattern 5: Ignoring Context (When, Where, With Whom)

**Description**: "Users struggle with setup" (generic) vs. "Users struggle with setup on their first day at a new company, using a personal laptop on the train, without IT support" (contextual).

**Why LLMs make this mistake**: Context requires lived experience or deep customer research. LLMs can infer generic problems but miss nuance.

**Guard**: For every problem statement, include: _When_ does it happen? _Where_ (which part of the user workflow)? _With whom_ (alone, with a manager, with IT)? What are they trying to accomplish?

## Quality Checklist

Before delivering the problem statement, verify:

- [ ] **Evidence-backed**: Every claim is supported by a direct quote, support ticket, or behavioral data; no "I assume" statements
- [ ] **Segment-specific**: Describes a particular customer group, not "everyone"
- [ ] **Solution-free**: No technology or feature recommendations; focuses on customer's underlying need
- [ ] **Quantified**: Includes how many customers, how often, business impact
- [ ] **Contextual**: Explains when, where, and why the problem occurs; what the customer is trying to accomplish
- [ ] **Surprising**: If your problem statement feels obvious or generic, dig deeper; there's usually more insight
- [ ] **Actionable**: The team can read this and immediately understand what research or design work to prioritize

## Further Reading

- Torres, Teresa. _Continuous Discovery Habits: Discover Products That Create Customer Value and底gain Competitive Advantage_. Product Talk, 2021.
- Christensen, Clayton M., Taddy Hall, Karen Dillon, and David S. Duncan. _Competing Against Luck: The Story of Innovation and Customer Choice_. HarperBusiness, 2016. Chapters 3-4 on jobs-to-be-done.
- Olsen, Dan. _The Lean Product Playbook: How to Innovate with Minimum Viable Products and Rapid Customer Feedback_. Wiley, 2015. Chapter 2 on problem selection.
- McFarland, Keith and Peter Diekmann. _The Bezos Letters: 14 Principles to Grow Your Business Like Amazon_. Harvard Business Review Press. On customer obsession and problem discovery.
- Cagan, Marty. _Inspired: How to Create Products Customers Love_. Wiley, 2008. Chapter 3 on customer discovery.
