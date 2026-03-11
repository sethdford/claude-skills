---
name: cost-of-delay
description: Quantify the business cost of delayed features to prioritize fast-payoff work.
---

# Cost of Delay

Calculate the business impact of delaying features to prioritize high-payoff work.

## Context

You are deciding what to build next. Cost of Delay quantifies the cost of waiting. Your goal is to prioritize work with high impact per week spent.

## Domain Context

- **Cost of Delay = opportunity cost**: Revenue lost, customer churn, competitive risk
- **Delay impact**: Some features become more valuable if delayed; others lose value
- **Cadence**: Fast shipping reduces total delay cost across portfolio
- **Risk of delay**: Competitive threats might close a window

## Instructions

1. **List opportunities**
2. **Estimate delay cost**: What's the monthly revenue/retention impact if we wait?
3. **Estimate effort**: Weeks to ship
4. **Calculate Cost of Delay / Effort**: Higher is more urgent
5. **Adjust for risk**: Add premium for competitive/strategic risk
6. **Prioritize**: Order by Cost of Delay / Effort

## Output Artifact

Cost of Delay analysis (1-2 pages):
- Opportunities with estimated delay costs
- Effort estimates
- Cost of Delay / Effort ratios
- Prioritized list with rationale
- Monthly revenue/churn impact if deprioritized

## Anti-Patterns

- **Confusing "important to me" with "high delay cost**: Strategic features might have low CoD
- **Not revisiting**: Delay cost changes; prioritization must change too
- **Ignoring waiting cost**: Cumulative delay cost adds up fast across portfolio
- **Assuming uniform delay**: Each week of delay has different cost (early weeks > later weeks)

## Further Reading

- *Inspired* (Marty Cagan) — prioritization
- *The Lean Product Playbook* (Dan Olsen) — opportunity assessment
