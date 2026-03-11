---
name: stakeholder-presentation
description: Present architecture to diverse audiences (executives, product, engineers). Tailor message, manage Q&A, handle skepticism. Use when communicating major decisions or visions.
---

# Stakeholder Presentation

Present architecture effectively to diverse audiences with tailored messaging and engagement.

## Context

You are presenting architecture to stakeholders. Tailor message for audience (executives care about cost/risk, engineers care about design). Anticipate objections. Manage time and questions.

## Domain Context

Based on presentation and communication best practices:

- **Executive Audience**: Lead with business impact (revenue, cost, risk). 20% architecture, 80% business. Numbers matter.
- **Technical Audience**: Design tradeoffs, implementation details, scalability. Respectful skepticism.
- **Product Audience**: Impact on feature velocity, user experience, reliability. Timeline and risk.
- **Presentation Skills**: Structure, pacing, visuals, energy. Engage audience, read room.

## Instructions

1. **Tailor to Audience**:
   - Executives: "This microservices architecture reduces deployment risk by 90% and lets us deploy 5x faster, reducing time-to-market by 4 weeks."
   - Engineers: "Services communicate via REST with circuit breakers, 3-second timeout, exponential backoff."
   - Product: "Architecture enables us to deploy payment service independently, reducing feature dependencies."

2. **Structure**:
   - Hook (why this matters)
   - Problem (what's broken)
   - Solution (how we fix it)
   - Impact (revenue, cost, speed, reliability)
   - Questions & Discussion

3. **Visuals**: Use diagrams (C4), not bullet points. Show architecture, data flow, scaling. One idea per slide.

4. **Manage Q&A**:
   - Tough question? "Great question, I'll come back to that." (Gives you time to think)
   - Don't know? "I don't know, but I'll find out and follow up."
   - Skepticism? Acknowledge, address directly. "You're right, that's a risk. Here's how we mitigate it."

5. **Follow-Up**: Send summary and decision. Record decisions, next steps, owners.

## Anti-Patterns

- **One-Size-Fits-All Presentation**: Same talk for executives and engineers. Result: one group lost, other bored. **Guard**: Customize per audience; keep different versions.
- **Death by Bullet Points**: 40 slides of text. Result: audience reads slides instead of listening. **Guard**: Visuals, not words; one idea per slide; speak, don't read.
- **Defensive on Questions**: Get flustered by skepticism. Result: lose credibility. **Guard**: Welcome tough questions; acknowledge valid concerns; address respectfully.
- **No Follow-Up**: Presentation ends, decision unclear, no next steps. Result: confusion, inaction. **Guard**: Summary email, clear decisions, owners, timeline.

## Further Reading

- _Presentation Zen_ by Garr Reynolds — visual communication
- _TED Talks: The Official TED Guide to Public Speaking_ — engaging audiences
- _Made to Stick_ by Chip and Dan Heath — memorable messaging
