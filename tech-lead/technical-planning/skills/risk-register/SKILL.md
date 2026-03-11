---
name: risk-register
description: Systematically identify and track technical and organizational risks that could impact delivery timelines. Use when planning significant initiatives.
---

# Risk Register

Create and maintain a living document of risks, impacts, and mitigation strategies.

## Context

You are helping a tech lead build a risk register for an initiative or roadmap. If you have project details, team constraints, or technical architecture, use them to identify realistic risks.

## Domain Context

- Project Management Institute (PMI): risk management is identifying, analyzing, and responding to risks that could impact project success
- Larson: "the best way to be wrong is confidently"; risk registers force healthy paranoia
- Nassim Taleb's "Antifragile": the goal is not to predict the future, but to be robust to surprises

Key principles:

1. **Risks are not problems**: A risk is something that might happen. If it has happened, it's a problem (manage differently)
2. **Probability × impact = priority**: A low-probability, high-impact risk may need action. A high-probability, low-impact risk might not
3. **Mitigation is not elimination**: You rarely eliminate risk. You reduce probability, reduce impact, or accept it

## Instructions

1. **Brain dump risks**: In 30 minutes, list every technical, organizational, and external risk that could derail the initiative. Don't filter; include paranoid ones. Example risks:
   - Key engineer leaves (headcount risk)
   - Third-party dependency (auth provider) changes their API (vendor risk)
   - Underestimated complexity in migration (technical risk)
   - Business priorities shift (strategy risk)
   - Infrastructure incident impacts development (operational risk)

2. **For each risk, estimate probability and impact**:
   - Probability: low (< 20%), medium (20-50%), high (> 50%)
   - Impact: low (can work around), medium (delays 1 sprint), high (derails project)

3. **Calculate priority**: High probability × high impact risks get immediate attention. Low probability × low impact risks get noted but not actively managed

4. **Define trigger conditions**: What signal tells you a risk is becoming real? Example: "If we haven't seen design by milestone X, architecture review risk is materializing"

5. **Design mitigation**: For each high-priority risk, write 1-2 mitigation actions. Focus on reducing probability (can we de-risk early?) or impact (what's our backup plan?). Example:
   - **Risk**: Key engineer leaves
   - **Mitigation 1**: Knowledge transfer sessions (pair programming) starting month 1, not month 3
   - **Mitigation 2**: Cross-train second engineer on critical path items now, while original engineer can mentor

6. **Assign owners**: Who monitors each risk and triggers mitigation if needed? Tech lead or specific engineer?

7. **Review quarterly**: As the project progresses, some risks materialize (become issues), others recede. Keep the register alive

Example format:

```
| Risk | Probability | Impact | Priority | Trigger | Mitigation | Owner |
|------|------------|--------|----------|---------|-----------|-------|
| Third-party auth API changes | Medium | High | High | API deprecation notice | Build abstraction layer, monitor API roadmap | Backend Lead |
| Capacity loss to firefighting | High | High | High | > 25% of sprint on interrupts | Define on-call rotation, reserve sprint slack | Tech Lead |
```

## Anti-Patterns

- **Generic risk lists**: LLMs sometimes generate boilerplate risks ("scope creep", "communication issues") without grounding them in the actual project. Always make risks specific to your context.
- **Assuming mitigation is free**: LLMs suggest mitigations (extra testing, documentation, pair programming) without accounting for the time cost. Good mitigations have a cost; list it explicitly.
- **Set-it-and-forget-it registers**: A risk register written in month 1 and never updated is useless. Require quarterly reviews and updates when probabilities change.
- **Treating all risks equally**: LLMs sometimes list 20 risks without prioritizing. Focus on the 3-5 risks that could actually derail the project. Ignore the rest.

## Further Reading

- PMI. "A Guide to the Project Management Body of Knowledge." 2021. Chapter on Risk Management.
- Taleb, Nassim. "Antifragile: Things That Gain from Disorder." Random House, 2012.
- Larson, Will. "An Elegant Puzzle." Chapter on managing uncertainty and risk in projects.
