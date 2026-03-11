---
name: documentation-strategy
description: Documentation levels and types (README, architecture, API, runbooks), keeping docs current and discoverable.
---

# Documentation Strategy

Planning documentation so engineers can find what they need.

## Context

You are planning documentation for a project or team. Multiple levels serve different needs.

## Domain Context

- **README**: First thing people read; quick start
- **Architecture**: How system is organized; key decisions
- **API Docs**: How to use services; generated from schema
- **Runbooks**: How to respond to alerts; specific procedures
- **ADR**: Why we chose this tech/approach; decisions recorded
- **HOWTO**: Step-by-step guides; "how do I deploy?"

## Instructions

1. **README**: Installation, basic usage, links to more docs
2. **Architecture**: System diagram, component responsibilities, data flows
3. **API**: Schema-driven docs; keep in sync automatically
4. **Runbooks**: One per alert; decision trees for diagnosis
5. **ADR**: Decisions recorded; future maintainers understand why
6. **Keep Current**: Outdated docs are worse than no docs
7. **Searchable**: Good naming, cross-links, table of contents

## Anti-Patterns

- Documentation in people's heads; knowledge walks out
- Scattered docs; team can't find them
- Out-of-date docs; misinformation spreads
- Too much prose; too little examples
- No diagrams; hard to visualize architecture
- No maintenance plan; docs decay

## Further Reading

- Diátaxis documentation framework (Procida)
- Google Technical Writing Course
- Write the Docs community
