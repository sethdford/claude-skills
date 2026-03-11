---
name: product-vision
description: Articulate a compelling, aspirational product vision that inspires teams, aligns stakeholders, and guides strategic decisions 3-5 years forward. Use when defining long-term direction, securing investment, or rallying teams around a north star.
allowed-tools: Read, Grep, Glob, Write, Edit
---

# Product Vision: Defining Your 3-5 Year North Star

Create a vision statement that paints a picture of the transformed future customers will experience, grounding it in real customer outcomes and market dynamics.

## Context

You are helping shape the future of a product. A vision is not a feature list or a mission statement—it's a picture of what the world looks like when the product has succeeded. A great vision inspires teams to take risks, guides tough trade-off conversations, and remains stable even as tactics shift.

Most visions fail because they're either too vague ("Be the leading platform") or too prescriptive (locked into one technology path). The best visions describe customer outcomes, not technical solutions.

## Domain Context

- **Marty Cagan's Vision vs. Mission**: Vision is the future state (3-5 years out); Mission is what the product does today
- **Inspired by customer outcomes, not technology**: Avoid "Use AI to..." visions that are solution-first, not problem-first
- **Testable assumptions**: A vision implies specific bets about customer behavior, market size, and competition
- **Ambitious but achievable**: Vision should feel like a stretch, but grounded in market reality and team capabilities
- **Durable across tactics**: Vision survives product pivots and feature changes; tactics (how we get there) change frequently

## When to Use This Skill

- You're founding a new product or business line and need to define long-term direction
- Your team has grown but lost alignment on "why are we building this?"
- You're seeking Series A/B funding and need to articulate the prize
- You're making a major strategic pivot and need to re-anchor the team
- You want to evaluate whether near-term opportunities (partnerships, features, pivots) align with your long-term vision

## Prerequisites

Before crafting a vision, gather:

1. **Customer research**: 10-20 interviews with customers showing unmet needs, jobs-to-be-done, workflows
2. **Market analysis**: Market size, growth trends, competitive landscape, future trends (consolidation, new platforms, regulatory change)
3. **Team perspective**: What excites engineers, designers, and leadership? What problems do they want to solve?
4. **Business constraints**: Revenue model, unit economics, capital needs, runway
5. **Historical context**: What worked and didn't in past products? What did customers value most?

If you're starting from scratch, spend 2-4 weeks researching before drafting vision.

## Instructions

### 1. Define the Customer Outcome (Not the Product)

Ask: "What will customers be able to do/achieve in 3-5 years that they can't today?"

Examples:

- ❌ "Build a mobile-first SaaS platform" (product-led)
- ✓ "Small teams manage their entire business (sales, ops, finance) without spreadsheets" (outcome-led)

### 2. Articulate the Shift

What's changing? Market? Customer behavior? Technology? Regulation?

Example: "Today, teams manually sync data across Salesforce, Stripe, and Google Sheets. In 3 years, teams will expect real-time data flow and automations that remove manual work."

### 3. Ground in Reality

Ask: "Is this achievable in 3-5 years given market trends, team capabilities, and capital?"

- Too ambitious: "Eliminate all BI tools" (requires disrupting entrenched incumbents)
- Realistic: "Make business intelligence accessible to non-technical users" (requires good UX and education)

### 4. Make It Inspiring

Read it aloud. Does it excite you? If it sounds like a corporate press release, rewrite it.

❌ "Empower customers to leverage synergies across platforms"
✓ "Teams will ship features 10x faster by eliminating toil from deployments, monitoring, and incident response"

### 5. Write the Vision Statement (1-3 sentences)

Conversational, aspirational, outcome-focused.

Example (Infrastructure automation):

> "In 3 years, every engineering team—from startups to enterprises—will deploy and scale applications with a single command. They'll spend zero time managing infrastructure, provisioning servers, or debugging deployment failures. They'll focus entirely on shipping product."

### 6. Define the Customer Outcome Enabled

Restate the customer benefit in measurable terms:

> "Developers ship 10x faster. Operations teams move from reactive firefighting to proactive optimization. Companies reduce infrastructure spend by 40% while increasing reliability."

### 7. Identify Market Assumptions

What bets is this vision making?

> - Assumption 1: Cloud adoption will reach 90% of enterprises by 2027
> - Assumption 2: Developers will increasingly choose managed services over self-hosted
> - Assumption 3: Cost and operational complexity remain the #1 reason companies adopt managed platforms

### 8. Draft the Roadmap Implication (How do we get there?)

High-level narrative (not detailed roadmap):

> "Year 1: Build core deployment platform with 80% of deployment scenarios covered. Win early-adopter startups.
> Year 2: Add observability and auto-scaling. Expand to mid-market. Build ecosystem of integrations.
> Year 3: Enterprise-grade features (audit logs, compliance, multi-region). Win enterprise accounts."

## Output Format

A 1-2 page vision document:

```
# [Product] Vision

## Vision Statement
[1-3 sentences describing the future customer state]

## Customer Outcome
[How does this change customers' lives? What becomes possible?]

## Market Shift
[What's changing in the market that makes this possible?]

## Strategic Bets
[Key assumptions about customer behavior, market trends, technology]

## Roadmap Narrative (3-5 years)
[High-level phases; major milestones]

## Success Metrics
[How will we know if we're on track? What would validate the vision?]

## What This Is NOT
[What opportunities we're explicitly NOT pursuing; what's out of scope]
```

## Worked Example

**Vision: Intelligent Customer Data Platform**

**Vision Statement**: "By 2027, every company—from SMBs to enterprises—will have a unified view of their customers across every touchpoint. Teams will act on customer insights instantly, without manual data work, APIs, or SQL queries."

**Customer Outcome**:

- Marketing teams eliminate wait time for customer segments; segments update in real-time
- Ops teams reduce time-to-ROI for new tools from 3 months to 2 weeks
- Data teams shift from building pipelines to designing customer experiences

**Market Shift**:

- Companies generate 10x more customer data than 5 years ago
- No-code/low-code tools are disrupting traditional data engineering
- Privacy regulations (GDPR, CCPA) require real-time data governance, not batch jobs

**Strategic Bets**:

- Assumption: Team composition will shift; non-technical marketers will need to access customer data
- Assumption: Real-time data is becoming table-stakes for retention/upsell
- Assumption: Existing data warehouse tools are too complex; a specialized CDP will win SMB/mid-market

**Roadmap Narrative**:

- **Year 1**: Build event ingestion and real-time segmentation. Win 100 early-adopter companies.
- **Year 2**: Add activation (integrate with email, SMS, Slack). Expand to 500+ customers. Build self-serve UX so teams don't need data engineering.
- **Year 3**: Add predictive intelligence (churn, LTV); expand to 2000+ customers. Become default CDP for non-enterprise companies.
- **Year 4**: Enterprise features (multi-tenant, audit logs, compliance). Win enterprise logos.

**Success Metrics**:

- ARR $100M+ (from $5M today)
- 50%+ of signups from non-data-intensive industries (proving non-technical adoption)
- NPS >50 (indicating customers love the product)
- <5% churn (proving sticky product-market fit)

**What This Is NOT**:

- We are NOT building a data warehouse replacement (that's Snowflake's job)
- We are NOT targeting data engineers; we're building for marketers and ops
- We are NOT competing on cost; we're competing on simplicity and outcomes

---

## Decision Framework

When drafting and facing uncertainty:

- **If the vision feels too vague**: Add specific customer outcomes. "Transform how companies manage growth" → "Every company will automatically personalize their product based on individual customer behavior"
- **If it feels too tied to one technology**: Rewrite in outcome language. "Build on Kubernetes" → "Teams will deploy at global scale with zero infrastructure maintenance"
- **If you can't articulate market shifts**: Research more. Vision requires understanding _why_ this future is possible now.
- **If the team doesn't react with energy**: It's not inspiring enough. Add tension, aspiration, or clarity.
- **If the vision seems achievable in <2 years**: It's not bold enough. You're describing a roadmap, not a vision.

## Anti-Patterns & Guards

### Anti-Pattern 1: Technology-First Vision

**Description**: "Leverage machine learning to..." or "Build on blockchain" (technology prescriptive) instead of "Eliminate manual customer matching" (outcome-focused).

**Guard**: If your vision mentions a technology, replace it with the customer outcome. Vision is timeless; technologies change.

### Anti-Pattern 2: Vague Mission Creep

**Description**: "Be the leading platform" (could mean anything) vs. "Every small business will manage customers, sales, and finance in one place" (specific).

**Guard**: Vision should be surprising/specific. If a competitor could claim the same vision, rewrite it.

### Anti-Pattern 3: Disconnected from Market

**Description**: Vision with no grounding in market trends, customer behavior, or technology evolution.

**Guard**: Every vision should articulate _why_ this future is possible now. What's changed?

### Anti-Pattern 4: Too Ambitious Without Path

**Description**: "Eliminate the need for data warehouses entirely" (attacking Snowflake's moat with zero differentiation).

**Guard**: Vision should be ambitious but grounded. You should be able to articulate a plausible path to winning.

### Anti-Pattern 5: Changing Vision Every Year

**Description**: Vision has short half-life; team can't plan or invest.

**Guard**: Vision should be stable for 3-5 years. Tactics change; vision doesn't.

## Quality Checklist

Before sharing the vision:

- [ ] **Outcome-focused**: Describes customer benefit, not technology or product features
- [ ] **Inspiring**: Reading it aloud makes team want to ship; not corporate/bland
- [ ] **Grounded in market**: Makes bets about market trends that are plausible
- [ ] **Testable**: Can articulate success metrics; would know if we're on track
- [ ] **Durable**: Would survive a major product pivot or technology change
- [ ] **Ambitious**: Feels like a stretch; 3-5 year timeline is appropriate
- [ ] **Specific**: Competitor couldn't claim the same vision
- [ ] **Aligned with business**: Model and strategy support this vision

## Further Reading

- Cagan, Marty. _Inspired: How to Create Products Customers Love_. Wiley, 2008. Chapters on vision and strategy.
- Lafley, A. G., and Roger L. Martin. _Playing to Win: How Strategy Really Works_. Harvard Business Review Press, 2013. On strategic clarity and choice.
- Rumelt, Richard. _Good Strategy, Bad Strategy: The Difference and Why It Matters_. Crown Business, 2011. On focus and coherence.
- Collins, Jim, and Jerry I. Porras. _Built to Last: Successful Habits of Visionary Companies_. HarperBusiness, 1994. On vision as organizational anchor.
