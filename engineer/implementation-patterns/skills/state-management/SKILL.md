---
name: state-management
description: Finite state machines, event sourcing, CQRS (Command Query Responsibility Segregation), and state modeling.
---

# State Management

Modeling and managing application state explicitly.

## Context

You are designing state management. Make state transitions explicit and predictable.

## Domain Context

- **FSM**: Finite state machine; explicit states and transitions
- **Event Sourcing**: Store events not state; replay to reconstruct
- **CQRS**: Separate read and write models; optimize independently
- **Immutable State**: State updates create new state objects

## Instructions

1. **Define States**: What states can your system be in? Be exhaustive
2. **Define Transitions**: What events trigger which transitions?
3. **Model Constraints**: What transitions are invalid? Encode in state machine
4. **Event Sourcing**: If you need audit trail, store events not state
5. **Separate Reads**: If read/write patterns differ, separate models
6. **Test Transitions**: Verify state machines work correctly

## Anti-Patterns

- Implicit state machine; state hidden in booleans ("isLoading", "hasError")
- No validation of transitions; invalid state becomes possible
- Mixing state and commands; separate concerns
- Event sourcing without strong typing; easy to replay wrong events
- CQRS when simple state suffices; adds complexity

## Further Reading

- Harel Statecharts (original, powerful FSM extension)
- Domain-Driven Design (Evans), Chapter on Aggregates
- CQRS Pattern (Microsoft docs)
