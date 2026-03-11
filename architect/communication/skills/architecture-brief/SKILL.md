---
name: architecture-brief
description: Write concise executive summaries of architecture. Communicate decisions and tradeoffs to non-technical stakeholders. Use when presenting to leadership or documenting decisions.
---

# Architecture Brief

Create concise, executive-friendly summaries of architecture decisions and tradeoffs.

## Context

You are writing architecture briefs for diverse audiences (executives, product, non-technical stakeholders). Explain decisions in business terms, not technical jargon. Emphasize impact on cost, speed, reliability.

## Domain Context

Based on effective technical communication:

- **Business Impact**: How does architecture choice affect time-to-market, cost, reliability? Quantify where possible.
- **Trade-offs**: Every architecture choice sacrifices something. Explicitly state: "We chose X over Y because Z matters more."
- **Risk Acknowledgment**: What could go wrong? Residual risks accepted. Mitigation plans for critical risks.
- **Assumptions**: What's true about our context that makes this choice right? Different context, different choice.

## Instructions

1. **One-Pager Structure**:
   - Title: "API Gateway Architecture for Microservices"
   - Problem: "Multiple services exposing APIs; no unified interface, inconsistent auth, no rate limiting"
   - Decision: "Implement API Gateway (Kong/AWS API Gateway)"
   - Rationale: "Centralizes auth, rate limiting, routing; 2-week implementation"
   - Trade-off: "Extra hop in request path (5ms latency); operational overhead of new service"
   - Success Metrics: "Consistent error responses, 99.9% uptime, < 50ms latency"
   - Risks: "Gateway becomes bottleneck (mitigation: auto-scaling, load testing)"

2. **Lead with Impact**: Start with business outcome. "This choice enables us to scale to 10x users without tripling ops team."

3. **Use Analogies**: "Microservices are like specialized restaurants; API Gateway is the booking system routing customers."

4. **Acknowledge Uncertainty**: "Based on current traffic and team size. If traffic changes 10x, we'll revisit."

5. **Make it Scannable**: Bullet points, bold key decisions. Executives should understand main point in 2 minutes.

## Anti-Patterns

- **Too Technical**: Explain implementation details, not impact. Result: non-technical readers lost. **Guard**: Lead with business impact; explain technical choice as supporting detail.
- **No Trade-offs Acknowledged**: "This is the best solution." Result: unrealistic, erodes trust. **Guard**: Always state what you're sacrificing; explain why.
- **Vague Success Metrics**: "It will be more scalable." Result: hard to measure success. **Guard**: Quantify: latency < 100ms, 99.99% uptime, < 5min deployment.
- **No Assumption Statements**: Assume everyone knows context. Result: brief is incomprehensible to new readers. **Guard**: Explain context explicitly.

## Further Reading

- _Made to Stick_ by Chip and Dan Heath — communicating complex ideas simply
- _Decisive_ by Chip and Dan Heath — presenting decision frameworks
- _Architecture Decision Records_ by Michael Nygard — documenting decisions clearly
