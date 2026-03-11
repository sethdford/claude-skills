---
name: context-diagram
description: Design high-level system boundary diagrams. Show external systems, users, data flows. Use when onboarding teams or clarifying system scope.
---

# Context Diagram

Create clear, high-level diagrams showing system boundaries and external interactions.

## Context

You are creating context diagrams to establish system scope. Show what's inside vs outside. Identify external dependencies and user interactions. Read system requirements and interfaces.

## Domain Context

Based on C4 model and systems thinking:

- **System Boundary**: What's included? Often misaligned between teams. Clear boundary prevents scope creep.
- **External Systems**: Payment processors, email services, third-party APIs. Owned by others; you depend on them.
- **Users/Actors**: Who uses the system? Customers, admins, automated systems. Different users have different interaction patterns.
- **Data Flows**: What data crosses the boundary? In what direction? Frequency? Synchronous or asynchronous?

## Instructions

1. **Draw Central Rectangle**: This is "your system" (e.g., "E-commerce Platform").

2. **Add External Systems**: Outside rectangle, show systems you depend on (Stripe for payments, SendGrid for email, AWS S3 for storage). Label communication protocol (REST, webhook, batch).

3. **Add Actors**: Customers (web browser), admins (internal tools), third-party integrations. Arrows show interaction direction and protocol.

4. **Label Data Flows**:
   - "Customer → Platform: Order request (REST, JSON)"
   - "Platform → Stripe: Payment (REST, HTTPS)"
   - "Platform → Email Service: Confirmation (REST, webhook)"

5. **Keep Simple**: One diagram, not multi-level. Aim for ~5-10 external entities. More = split into smaller diagrams or go to container level.

## Anti-Patterns

- **Too Detailed**: Show internal components in context diagram. Result: defeats purpose of high-level view. **Guard**: Only show external systems and major actors.
- **Unclear Boundaries**: "Is authentication part of the system?" Result: confusion. **Guard**: Explicitly define what's in/out. If shared, explain ownership.
- **No Data Flow Labels**: Assume readers know what data flows. Result: ambiguity. **Guard**: Label every arrow: "Customer data (GDPR-sensitive)", "Metrics (non-sensitive)".
- **Outdated Diagram**: New external integration added, diagram not updated. Result: wrong mental model. **Guard**: Update when external dependencies change; periodic review.

## Further Reading

- _C4 Model for Software Architecture_ by Simon Brown — context diagram patterns
- _System Thinking_ by Peter Senge — boundary definition and system interactions
- _Domain-Driven Design_ by Eric Evans — context and bounded contexts
