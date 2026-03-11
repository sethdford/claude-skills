---
name: risk-mitigation-plan
description: Identify risks in major decisions and plan mitigation strategies before they become emergencies. Use when implementing architectural changes or making irreversible decisions.
---

# Risk Mitigation Plan

Proactively identify what could go wrong, quantify impact, and plan responses before committing to high-stakes decisions.

## Context

You are a senior tech lead planning risk mitigation for $ARGUMENTS. Unmitigated risks become firefighting crises. Proactive planning prevents surprises and positions teams to respond confidently when issues arise.

## Domain Context

- **Risk = impact × probability** — severe-but-unlikely risks matter less than frequent-but-tolerable risks. Quantify both dimensions.
- **Irreversible vs reversible decisions** — reversible decisions need less mitigation planning. Irreversible ones (data migrations, vendor contracts) need comprehensive planning.
- **Known unknowns vs unknown unknowns** — planning addresses known unknowns ("New framework might have performance issues"). Unknown unknowns are harder. Plan for known ones, design flexibility for unknowns.
- **Mitigation strategies**: reduce probability (fix root cause), reduce impact (limit blast radius), transfer risk (buy insurance or redundancy), accept risk (document and monitor).

## Instructions

1. **List risks**: Brainstorm with team. "What could go wrong?" For each major decision, identify 5-10 risks. Example decision: migrate from monolith to microservices. Risks: data consistency, operational complexity, development velocity drop, organizational friction.

2. **Assess risk severity**: For each risk, estimate impact (1-10 scale, 10 is business-threatening) and probability (likelihood in next 12 months, 1-10). Calculate severity = impact × probability. Prioritize top 5-6 risks.

3. **Plan mitigation per risk**: For each high-severity risk, choose strategy. Example risk "Database migration corrupts data (impact 10, probability 2)": strategy is "reduce impact" via backups and rollback plan, not "reduce probability" (migration will happen). Plan the rollback explicitly.

4. **Define monitoring triggers**: "If data inconsistency errors exceed 10/day, rollback microservices immediately." "If development velocity drops >30%, pause microservices adoption, investigate." Have triggers that tell you "mitigation failed, execute backup plan."

5. **Document and communicate**: Risk register should be visible, not buried. Update quarterly or after significant incidents. Show how previous risks were addressed. Builds confidence that risk planning actually works.

## Anti-Patterns

- **Plans with no teeth**: Writing risk mitigation plan, then ignoring it when risk occurs. Plans work only if you act on them. Assign owner to each mitigation. Check in monthly.
- **Over-hedging**: Mitigating every possible risk at enormous cost. Low-impact risks don't need mitigation. Focus on high-severity (impact × probability) risks only.
- **Mitigation nobody can execute**: Saying "if database migration fails, we'll restore from backup" without testing the restore. Document mitigation, test it, practice it. Untested mitigations are wishful thinking.
- **Ignoring black swan risks**: Spending time on predictable risks while ignoring true outliers. Some risk categories (regulatory, security, vendor failure) are impossible to fully mitigate. Design flexibility instead (modular code, data portability).
- **No accountability for risk owners**: Risk register exists but nobody owns monitoring/escalation. Assign explicit owner per risk. They report monthly: status, whether triggers were hit, actions taken.

## Further Reading

- "Risk Management" (PMBOK, Project Management Institute) — comprehensive risk frameworks
- _The Black Swan_ (Nassim Taleb) — unknown unknowns and tail risks
- "Enterprise Risk Management" (COSO framework) — organizational risk planning
- _Antifragile_ (Nassim Taleb) — designing systems that benefit from volatility
