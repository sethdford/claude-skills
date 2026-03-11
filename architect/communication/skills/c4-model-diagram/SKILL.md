---
name: c4-model-diagram
description: Create C4 context, container, component, and code diagrams. Visualize architecture at different abstraction levels. Use when communicating system structure to diverse audiences.
---

# C4 Model Diagram

Create C4 diagrams to communicate architecture at multiple abstraction levels.

## Context

You are creating architecture diagrams. Use C4 model for consistent representation. Start at highest level (context), zoom in progressively (container, component, code). Read architecture decisions and system structure.

## Domain Context

Based on Simon Brown's C4 model:

- **Context Diagram**: System in environment. Shows external systems, users, data flows. Answers: "What is this system?"
- **Container Diagram**: Major building blocks (web app, database, API, message queue). Answers: "What's inside the system?"
- **Component Diagram**: Internal structure of container. Shows responsibilities, communication. Answers: "How is [container] organized?"
- **Code Diagram**: Class diagram for specific component. Shows classes, methods, relationships. Answers: "What does [component] contain?"

## Instructions

1. **Draw Context Diagram**: Rectangle for your system. External systems (payment provider, email service). Actors (user, admin). Label data flows. Answers "What does this system do?"

2. **Draw Container Diagram**: Inside system rectangle, show containers (web app, API, database, cache). Interfaces between containers. Technology choices (PostgreSQL, Redis). Answers "What technology?"

3. **Draw Component Diagram**: Pick one container (API). Inside, show components (auth service, payment service, order service). Responsibilities, communication patterns.

4. **Draw Code Diagram**: For complex component, show classes, methods. Use standard UML or pseudo-code. Limit to critical logic; don't over-document.

5. **Keep Diagrams Current**: As architecture evolves, update diagrams. Outdated diagrams mislead teams. Use tools (draw.io, Structurizr, Miro) that allow collaboration and versioning.

## Anti-Patterns

- **One Massive Diagram**: Try to show everything in one diagram. Result: unreadable, overwhelming. **Guard**: Use C4 levels; zoom progressively.
- **Diagrams Without Legend**: Assume readers know what symbols mean. Result: confusion. **Guard**: Label technologies, responsibilities, data flows clearly.
- **Outdated Diagrams**: Never update as system evolves. Result: teams follow wrong architecture. **Guard**: Update during architecture reviews; treat as living document.
- **Too Much Detail Too Early**: Start with code diagram. Result: lost in details before understanding system shape. **Guard**: Start at context; zoom in gradually; leave code diagram optional.

## Further Reading

- _The C4 Model for Software Architecture_ by Simon Brown — foundational reference
- _Software Architecture in Practice_ by Len Bass et al. — visualization best practices
- _Communicating Software Architecture_ — architecture documentation patterns
