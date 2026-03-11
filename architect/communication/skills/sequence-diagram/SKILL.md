---
name: sequence-diagram
description: Show interactions and flows over time. Illustrate request paths, asynchronous patterns, error handling. Use when documenting complex flows or onboarding on system behavior.
---

# Sequence Diagram

Visualize interactions and message flows between components over time.

## Context

You are creating sequence diagrams to explain how components interact. Show request/response patterns, timing, error handling. Read flow requirements and interaction sequences.

## Domain Context

Based on UML sequence diagrams and flow documentation:

- **Synchronous Flow**: Client calls service, waits for response. Simple, but blocking.
- **Asynchronous Flow**: Client sends message, continues without waiting. Service processes later, responds via callback/event.
- **Error Handling**: Happy path and error paths. Timeouts, retries, circuit breakers.
- **Sequence**: Order of interactions matters. Some flows have dependencies (A before B before C).

## Instructions

1. **Identify Actors**: Services, external systems, users involved. List vertically on left.

2. **Draw Time Axis**: Vertical axis = time (top to bottom = early to late).

3. **Draw Interactions**:
   - Solid arrow = synchronous request (waits for response)
   - Dashed arrow = asynchronous message (fire-and-forget)
   - Label arrow with message name and data

4. **Example: Order Processing**:

   ```
   Customer → API: POST /orders (order_id, items)
   API → Database: INSERT order (async)
   API → Payment Service: Charge card (sync)
   Payment Service → Stripe: POST /charges
   Stripe → Payment Service: 200 OK
   Payment Service → API: 200 OK
   API → Customer: 200 OK (order_id)
   Database → Event Service: order.created event (async)
   Event Service → Email Service: Send confirmation
   ```

5. **Add Alternatives**: Show error cases. "If payment fails, rollback order. If timeout, retry with exponential backoff."

## Anti-Patterns

- **Too Complex Diagram**: Show 20 interactions. Result: unreadable. **Guard**: Focus on one flow; use multiple diagrams for different scenarios.
- **Only Happy Path**: Never show errors or timeouts. Result: incomplete understanding. **Guard**: Include error cases, retries, timeouts.
- **No Timing Information**: Arrows all look the same. Result: unclear latency impact. **Guard**: Label latency-critical interactions; note timeouts.
- **Outdated Sequence**: Flow changed (new retry logic, new service), diagram not updated. Result: wrong mental model. **Guard**: Update when flow changes; document in comments.

## Further Reading

- _UML 2 Sequence Diagrams_ — formal sequence diagram syntax
- _Enterprise Integration Patterns_ by Gregor Hohpe — message flow patterns
- _Documenting Software Architecture_ — flow visualization best practices
