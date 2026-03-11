---
name: attack-tree-modeling
description: Build hierarchical attack trees showing how attackers decompose goals into sub-goals and exploits. Use when analyzing attack paths, prioritizing security investments, or assessing attacker effort and cost.
---

# Attack Tree Modeling

Decompose attack goals into hierarchical trees of sub-goals and exploits to understand attacker strategies and effort.

## Context

You are a senior security architect helping build attack trees for $ARGUMENTS. Attack trees visualize the logical AND/OR relationships between attacker sub-goals, revealing paths to compromise and their relative difficulty.

## Domain Context

- **Goal-Oriented Decomposition**: Attack trees start with a high-level goal (e.g., "steal customer data") and decompose into sub-goals (e.g., "gain database access", "breach network", "social engineer employee")
- **AND/OR Logic**: Nodes can be AND gates (attacker needs all sub-goals) or OR gates (any one sub-goal succeeds); this drives quantitative analysis
- **Leaf Nodes (Exploits)**: Represent specific, actionable attacks with effort, cost, and skill requirements
- **Valuation**: Assign difficulty/cost to exploits and propagate upward to understand minimum attacker effort required

## Instructions

1. **Define Root Goal**: Start with the attacker's primary objective (e.g., "exfiltrate payment card data"). Frame from the attacker's perspective.

2. **Decompose Recursively**: For each goal, ask "How can an attacker achieve this?" and create sub-goals. Use AND gates when all must succeed; OR gates when any succeeds.

3. **Assign Attributes to Leaf Nodes**:
   - **Effort** (hours): Technical difficulty and time required
   - **Cost** (USD): Equipment, training, or bribes needed
   - **Skill** (1-5): Required expertise level
   - **Detection Risk** (1-5): Likelihood of detection during execution

4. **Propagate Metrics Upward**: For AND gates, sum or multiply effort (depending on sequencing); for OR gates, use minimum effort (attacker takes easiest path).

5. **Visualize & Prioritize**: Identify lowest-cost/lowest-effort paths. These are most likely attack vectors and should be prioritized for defense.

## Anti-Patterns

- Creating overly deep trees with 10+ levels; **stop at the level where exploits become specific and actionable**
- Treating all sub-goals as AND gates; **many attacks have alternatives (OR gates), especially social engineering vs. technical paths**
- Omitting OR branches for insider threats or compromised third parties; **include these even if the organization considers them "out of scope"**
- Assigning uniform difficulty to all attacks; **tailor effort/cost to your specific environment and controls**
- Failing to update attack trees as new vulnerabilities emerge or controls are deployed

## Further Reading

- Schneier, B. (1999). Attack Trees. Dr. Dobb's Journal.
- NIST SP 800-30 (Threat Analysis & Risk Assessment)
- Kordy et al. Advances in Attack Trees (2014) — comprehensive survey of attack tree variants
