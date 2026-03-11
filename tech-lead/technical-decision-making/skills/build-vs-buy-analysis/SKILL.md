---
name: build-vs-buy-analysis
description: Systematically evaluate whether to build custom solutions or buy/adopt existing products. Use when facing major make-or-buy decisions on infrastructure, tooling, or features.
---

# Build vs Buy Analysis

Create frameworks to avoid both the curse of custom-building everything and the trap of adopting ill-fitting products.

## Context

You are a senior tech lead evaluating build vs buy for $ARGUMENTS. Both extremes are costly: building everything means slow shipping and technical debt; buying everything means feature misfit and vendor risk.

## Domain Context

- **Core vs context** (Geoffrey Moore) — build competitive advantage (core), buy or commoditize everything else (context).
- **Build if unique advantage** — if custom solution gives durable competitive edge, build it. If everyone's solution works equally well, buy.
- **Time-to-value matters** — buying gets you functional in weeks; building takes months. Early market position can be worth more than perfect fit.
- **Total cost analysis** — buying: licensing + integration + training. Building: dev effort + maintenance + hiring. Include opportunity cost of engineering time.

## Instructions

1. **Define decision criteria matrix**: Include: time-to-market (weeks to deliver), cost (total 5-year cost), team capability (can we build/operate this?), vendor risk (dependency on external company), differentiation (does custom solution unlock advantage?), flexibility (ease of changing later).

2. **Score build option**: Estimate engineering hours to build, maintain, and operate. Include learning curve for team. If feature will be 50% of one senior engineer for 2 years, cost is ~500K + risk. Add 30% buffer for unforeseen complexity.

3. **Score buy option**: List vendors. Get quotes. Include integration work, onboarding, training. Multiply license cost by 3 to account for full burden. Evaluate vendor stability and lock-in risk.

4. **Quantify differentiation**: Does building this unlock revenue, defensibility, or capability competitors can't easily replicate? If no, strongly prefer buying. If yes, weigh advantage against cost.

5. **Document decision and review trigger**: "We chose to buy X on $DATE because $REASON. If $CONDITION happens (new vendor emerges, requirements change), revisit decision in Q3."

## Anti-Patterns

- **Build bias**: "We can build it cheaper/faster/better" rarely holds. Engineers underestimate maintenance cost 60% of the time. Maintenance compounds over years. Include maintenance in estimates.
- **Lock-in blindness**: Buying software that's hard to exit from (data format, API coupling, vendor dependency). Medium-term pain exceeds short-term savings. Evaluate exit cost upfront.
- **Ignoring opportunity cost**: "Building this costs 1 engineer for a year" sounds cheap. But that engineer could build revenue-generating features. Opportunity cost often exceeds direct cost.
- **Perfect-is-enemy-of-good**: Waiting for ideal product because none fits 100%. Off-the-shelf product that covers 85% of needs is usually better than custom 100%. Accept "good enough."
- **No revisit cadence**: Making a build/buy decision once, then never reconsidering. Markets shift. Revisit every 2-3 years for critical components.

## Further Reading

- "Build vs Buy" (Paul Daugherty, Accenture) — TCO frameworks
- *Only the Paranoid Survive* (Andy Grove) — core vs context decision-making
- "Make vs Buy Analysis" (Harvard Business Review) — decision frameworks
- *The Goal* (Goldratt) — constraint thinking in make-or-buy decisions
