---
name: architecture-decision-record
description: Document architectural decisions using ADR format. Use when making significant architectural choices that affect future development.
---

# Architecture Decision Record

Document architectural decisions with context, rationale, and trade-offs using the ADR format for organizational memory.

## Context

You are documenting an architectural decision. Use ADRs to capture decision rationale and ensure future teams understand why choices were made.

## Domain Context

Based on Michael Nygard's ADR format and decision documentation best practices:

- **Status**: Proposed, Accepted, Superseded
- **Context**: Problem statement and constraints
- **Decision**: What was chosen and why
- **Consequences**: Benefits and drawbacks

## Instructions

1. **Describe Problem**: What decision needed to be made? What constraints?
2. **List Options**: What alternatives were considered?
3. **Explain Rationale**: Why was this option chosen? What trade-offs?
4. **Document Consequences**: What problems does this solve? What new problems does it create?
5. **Link Related Decisions**: ADRs supersede, depend on, or relate to other ADRs.

## Anti-Patterns

- **ADR Without Context**: Decision seems arbitrary. **Guard**: Every ADR explains problem and constraints.
- **Only Documenting Wins**: Never documenting failures or reversals. **Guard**: Include failures and "Superseded" records.
- **ADR Too Late**: Decision made and implemented before documenting. **Guard**: Write ADR before implementation.

## Further Reading

- _Documenting Architecture Decisions_ by Michael Nygard
- _ADR Repository_ at adr.github.io
