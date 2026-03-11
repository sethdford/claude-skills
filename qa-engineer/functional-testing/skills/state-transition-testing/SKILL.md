---
name: state-transition-testing
description: Design tests from state machine models to verify correct transitions, guard conditions, and invalid state handling. Use for workflows, UI flows, protocols, and stateful components.
---

# State Transition Testing

Model system behavior as finite state machines and derive tests that verify every valid transition fires correctly, every guard condition is enforced, and every invalid transition is properly rejected.

## Context

You are a senior QA engineer designing state transition tests for $ARGUMENTS. This black-box technique is essential for any component with distinct states and event-driven behavior.

## Domain Context

- **ISTQB Foundation Syllabus (4.2.4)**: State transition testing is a formal black-box technique. Coverage levels range from 0-switch (all transitions) to N-switch (transition sequences of length N)
- **ISO/IEC 25010**: Functional correctness requires that all specified state transitions produce correct outputs and that unspecified transitions are handled safely
- **UML State Machine Diagrams** (OMG UML 2.5): Provide standard notation for states, transitions, guards, actions, and composite states
- **Mealy vs. Moore machines**: Outputs depend on transition (Mealy) or state (Moore) — this distinction affects where to place assertions

## Instructions

1. **Model the state machine**: Identify all states, events/triggers, guard conditions, actions, and transitions. Draw the state transition diagram or build a state transition table. Include initial state, terminal states, and error/recovery states
2. **Build the state transition table**: Create a matrix with current states as rows and events as columns. Each cell contains the next state and action. Empty cells represent invalid transitions — these are test targets too
3. **Derive 0-switch coverage tests**: Write one test for each valid transition in the table. Each test: set up the precondition state, trigger the event, assert the new state and action output
4. **Derive 1-switch coverage tests**: Write tests for pairs of consecutive transitions (transition sequences of length 2). These catch defects where state A→B works and B→C works, but A→B→C fails due to residual state
5. **Test invalid transitions**: For every empty cell in the state transition table, attempt the event in that state and verify the system rejects it gracefully — no state corruption, proper error message, system remains in the original state
6. **Test guard conditions**: For transitions with guards, test both the true and false paths. Verify the guard evaluation uses correct data and that boundary values of guard conditions are tested

## Anti-Patterns

- **Incomplete state identification** — LLMs model only the "happy path" states and miss error states, timeout states, suspended states, and partially-completed states. **Guard:** Ask "what happens if the process is interrupted at this point?" for every state to discover hidden states.
- **Ignoring invalid transitions** — LLMs focus on valid paths and forget that testing what _shouldn't_ happen is equally important. **Guard:** Every empty cell in the state transition table must have at least one negative test case.
- **Conflating state with data** — LLMs confuse changing data values with state transitions (e.g., treating "balance updated" as a state change). **Guard:** States must represent qualitatively different behaviors, not just different data values. If the system responds identically to all events regardless of a "state" change, it's not a real state.

## Further Reading

- ISTQB Foundation Level Syllabus, Section 4.2.4 — State transition testing technique and coverage criteria
- Harry Robinson, "Finite State Model-Based Testing on a Shoestring" — Practical state machine test generation
- Lee & Yannakakis, "Principles and Methods of Testing Finite State Machines" — Academic foundation for conformance testing
- Robert Binder, _Testing Object-Oriented Systems_ — State-based testing patterns for OO systems

---
