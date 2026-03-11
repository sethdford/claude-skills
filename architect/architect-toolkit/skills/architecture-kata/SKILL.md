---
name: architecture-kata
description: Practice architectural design with structured problems. Time-limited design challenges. Use for skill development, interviews, team exercises.
---

# Architecture Kata

Practice architectural design through structured, time-limited design challenges.

## Context

You are working on architecture kata. Design a system within constraints (time, technology, team). Iterate on design, gather feedback, refine. Read problem statement and constraints carefully.

## Domain Context

Based on architecture kata format (similar to code kata, but for design):

- **Problem Statement**: Requirements, constraints, scale, non-functional requirements
- **Time Box**: 30 minutes to 2 hours. Forces focus and trade-off decisions.
- **Constraints**: Limited technology choices, team size, deployment options. Realistic constraints teach design skill.
- **Feedback**: After kata, discuss solution with peers/mentor. Learn from different approaches.

## Instructions

1. **Read Problem**: Understand requirements. What's the core business problem? What's the scale? What's non-negotiable?

2. **Identify Constraints**: Technology choices? Team size? Deployment platform? Time-to-market? These shape design.

3. **Quick Design** (15-30 min):
   - Sketch components/services
   - Identify data model
   - Show communication patterns
   - Call out risks/trade-offs

4. **Document Decisions**: Why this architecture? What trade-offs made? What would you do differently at 10x scale?

5. **Discuss & Refine**: Present to peer or mentor. What would they do differently? Why? Learn from different perspectives.

## Anti-Patterns

- **Analysis Paralysis**: Spend 30 minutes debating one decision. Result: no design in time box. **Guard**: Make quick decisions; iterate after.
- **Overengineering**: Design for 100x scale when problem is tiny. Result: complex, doesn't teach. **Guard**: Design for stated requirements; note what changes at 10x.
- **No Constraints**: Assume unlimited budget/time/team. Result: not realistic. **Guard**: Use constraints to learn prioritization.
- **No Discussion**: Design alone, never discuss. Result: miss learning. **Guard**: Share, discuss, learn from others' approaches.

## Further Reading

- _Architecture Kata_ by Neal Ford and Mark Richards — structured design exercises
- _Building Microservices_ by Sam Newman — design patterns through examples
- _Growing Object-Oriented Software, Guided by Tests_ — iterative design practice
