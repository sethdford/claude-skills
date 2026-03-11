---
name: spike-plan
description: Design research spikes to investigate technical uncertainty before committing to large implementation efforts. Use when feasibility is unclear or approach is unproven.
---

# Spike Plan

Use time-boxed research to de-risk unknowns, explore solutions, and validate assumptions before major implementations.

## Context

You are a senior tech lead planning a spike for $ARGUMENTS. Spikes answer "Can we do this?" before "How do we do this?" They compress learning into 1-2 weeks, preventing 3-month implementation detours.

## Domain Context

- **Bounded exploration** — spikes are timeboxed (1-2 weeks max). If you can't answer the key question in that time, you need an even shorter spike.
- **Throw-away code** — spike code is research, not production. Don't refactor it for production. Write new code after spike concludes. Spike code teaches, not ships.
- **Questions drive spikes** — "Will library X integrate with our stack?" is spiking. "Build a production integration" is implementing. Start with a question, not an outcome.
- **Assumptions cascade** — one assumption tested → multiple assumptions revealed. Spikes are assumption-hunting exercises.

## Instructions

1. **Define the spike question**: "Can we achieve target latency with technology X?" not "Build search system." Narrow focus. Spike should be answerable in 1-2 weeks with 1-2 engineers. Too broad = unlimited scope.

2. **Set explicit boundaries**: Time (1-2 weeks), scope (proof of concept, not production), team (1-2 people), success criteria (answer the question, not build the feature). Write these down. Prevents scope creep.

3. **Design learning experiments**: List 3-5 experiments that test the core assumption. Example spike: "Does Kafka fit our use case?" Experiments: setup cluster locally, write/read at target throughput, test fault tolerance, measure ops overhead.

4. **Run experiments rapidly**: Build smallest possible test. If you can test with CLI, don't write code. If you can test with 1 hour of exploration, don't spend a day building. Maximize learning per hour.

5. **Document findings and decision**: Spike concludes with writeup: question asked, experiments run, findings, recommended path forward. "We found Kafka meets perf needs but operational complexity is higher than RabbitMQ. Recommend RabbitMQ with planned migration to Kafka in 18 months."

## Anti-Patterns

- **Spikes become projects**: Spike to "explore search" becomes 3-week production implementation. Prevents other work. Timeboxing doesn't hold. Cancel spike at deadline, assess learnings, decide next step separately.
- **Wrong scope for spike**: Spiking on "build distributed system" is too broad. Spike on "does this consensus algorithm meet latency requirements?" is right size.
- **Spike code shipped**: Using spike prototype as production foundation. Quality was never priority. Rewrite after spike concludes. Prototype teaches, not ships.
- **No decision trigger**: Running spike but not defining upfront what answers kill the approach. Ambiguous results lead to "let's explore more." Define kill criteria upfront. If assumptions aren't met, pivot.
- **Ignoring second-order learning**: Spike on technology A reveals that concern B matters. Write that down. Future decisions depend on it.

## Further Reading

- "Spikes in User Stories" (Mike Cohn, Mountain Goat Software) — spike techniques
- _Innovator's Dilemma_ (Christensen) — bounded exploration and decision-making
- "Technical Debt and Spikes" (Martin Fowler) — exploratory coding patterns
- _Rapid Development_ (McConnell) — investigation overhead and risk management
