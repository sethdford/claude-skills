---
name: interview-prep
description: Prepare for architecture interview questions and scenarios. Practice system design, tradeoff discussions, communication. Use for career development and interview readiness.
---

# Interview Prep

Prepare for architecture interview questions and system design scenarios.

## Context

You are preparing for architecture interviews. Practice system design problems, articulate trade-offs, communicate clearly under pressure. Study common patterns and real-world constraints.

## Domain Context

Based on architecture interview best practices:

- **System Design Questions**: "Design Instagram", "Design distributed cache", "Design payment system"
- **Communication Skills**: Clarify requirements, think out loud, accept feedback, adjust design
- **Trade-off Discussion**: Consistency vs availability, latency vs cost, flexibility vs simplicity
- **Real-World Constraints**: Assume realistic team size, budget, deployment platform

## Instructions

1. **Study Common Systems**:
   - Social media (Facebook, Instagram): scale, feed generation, notifications
   - Payments (Stripe, PayPal): transactions, fraud detection, reconciliation
   - Search (Google): indexing, ranking, distributed retrieval
   - Messaging (WhatsApp, Slack): realtime, reliability, scalability

2. **Practice System Design Problem**:
   - Clarify: Scale (1M users, 1B records)? Growth (100x in 2 years)? Consistency (strong or eventual)?
   - Sketch: Components, data model, communication, scaling strategy
   - Discuss: What would you change at 10x scale? Where are bottlenecks? What are risks?

3. **Prepare Answers to Common Questions**:
   - "How would you scale this to 10x?"
   - "How does this fail?"
   - "What's the biggest risk?"
   - "How would you monitor this?"
   - "What would you do differently with more resources?"

4. **Practice Communication**:
   - Think out loud. "I'm thinking about SQL vs NoSQL because..."
   - Accept feedback. "Good point, that would break my design. Let me reconsider..."
   - Ask clarifying questions. "How much data? How many users? What's the latency requirement?"

5. **Mock Interviews**: Practice with peer or mentor. Get feedback on communication, technical depth, trade-off reasoning.

## Anti-Patterns

- **Memorized Answers**: Recite template answer. Result: inflexible, obvious. **Guard**: Understand reasoning; be ready to adapt.
- **Over-Engineering**: Design Netflix-scale system for startup problem. Result: miss point of interview. **Guard**: Scale to stated requirements; note evolution path.
- **No Communication**: Silently design, then present finished design. Result: interviewer can't assess thought process. **Guard**: Think out loud; engage interviewer; ask questions.
- **Defensive on Feedback**: Interviewer suggests different approach, you defend yours. Result: seems arrogant. **Guard**: Listen, consider, adjust; good solutions are collaborative.

## Further Reading

- _Designing Data-Intensive Applications_ by Martin Kleppmann — patterns and tradeoffs
- _System Design Interview_ by Alex Xu — interview-specific guidance
- _The Art of Scalability_ by Martin Abbott — scaling patterns
