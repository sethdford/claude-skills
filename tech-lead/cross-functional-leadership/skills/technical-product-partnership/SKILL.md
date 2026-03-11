---
name: technical-product-partnership
description: Build collaborative relationships with product managers where engineers shape strategy and product makes informed decisions about technical tradeoffs. Use when coordinating feature prioritization or platform decisions.
---

# Technical-Product Partnership

Build relationships where product and engineering are true partners, not adversaries debating feature vs technical debt.

## Context

You are a senior tech lead partnering with product for $ARGUMENTS. Poor partnerships result in engineering debt accumulation or missed features. Good partnerships align incentives: both win when shipping features with good fundamentals.

## Domain Context

- **Incentive alignment** — product is measured on features shipped, engineering on velocity/quality. Misaligned incentives create conflict. Align by making tech debt impact feature velocity visible.
- **Debt compounds** — cutting corners saves 1 week short-term but costs 3 weeks long-term (via slowdown). Product needs to see that graph. Data changes conversations.
- **Platform thinking** — share vision of how 12-month platform investment enables next 24-month feature pipeline. Product managers think quarterly; tech leads think years ahead.
- **Influence without authority** — tech lead can't dictate to product, but can inform decisions. Best partnerships use data to show tradeoffs, let PM decide with full context.

## Instructions

1. **Establish shared metrics**: Define metrics both care about. Not "tech debt reduction" (product doesn't care) or "features per quarter" (engineering can't sustain that forever). Instead: "cycle time to ship feature," "production incident count," "customer satisfaction." Both benefit from improvement.

2. **Visibility into technical roadmap**: PM should see 3-6 month technical plan alongside feature roadmap. "Refactor database layer (2 sprints)" not "do tech debt." PM understands investment, can prioritize appropriately.

3. **Educate on tradeoffs**: When proposing feature, show technical implications. "Feature X is 2 weeks with current architecture or 5 weeks if we refactor first. Refactor unlocks 4 future features. Recommendation: refactor first." PM can decide with full info.

4. **Create decision frameworks**: "We approve technical debt if it enables 3+ features or reduces cycle time by 20%." Documented framework prevents repeated negotiation.

5. **Regular alignment meetings**: Weekly/biweekly check-in on feature progress, technical blockers, priority changes. Informal partnership maintenance prevents surprises.

## Anti-Patterns

- **Engineering vetoes features**: Tech lead saying "that's not feasible" without exploring. Better: "That's complex, here are 3 approaches: fast-but-risky, slow-but-sound, middle-ground. PM chooses."
- **Product cuts all technical investment**: "Debt reduction can't happen; features are blocked until profit targets met." Eventually system collapses under debt. Tech lead needs to fight here with data.
- **One-sided influence**: Product dictates roadmap, engineering executes without voice. No partnership. Tech lead should have seat at prioritization table.
- **No economic transparency**: PM doesn't see cost of tech choices. "Why did shipping take 3x longer?" is frustration without context. Visualize cost in PM's language (features, velocity, risk).
- **Ignoring product constraints**: Tech lead proposes 6-month refactor while PM needs feature in 4 weeks. Partnerships require trade-offs and pragmatism, not technical purity.

## Further Reading

- "Technical Product Strategy" (Reforge) — aligning engineering and product vision
- _Inspired_ (Marty Cagan) — product strategy and team dynamics
- "Engineering Ladders" (Will Larson) — IC influence and partnerships
- "Technical Debt" (Martin Fowler) — communicating debt to non-engineers
