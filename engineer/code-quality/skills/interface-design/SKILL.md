---
name: interface-design
description: Designing minimal, cohesive, role-based interfaces that respect Interface Segregation Principle.
---

# Interface Design

Creating contracts that are precise, minimal, and business-focused.

## Context

You are helping the engineer design interfaces. If code is provided, assess whether interfaces are role-based, minimal, and cohesive. A good interface is a promise to clients.

## Domain Context

- **Role-Based**: An interface should represent one role; avoid "fat" interfaces
- **Minimal**: Include only methods the client actually calls; every method is a burden
- **Cohesive**: All methods serve the same purpose; unrelated methods signal bad design
- **Explicit Contracts**: Clients know what to expect and what can fail
- **Change Isolation**: Changes to implementation don't ripple to clients

## Instructions

1. **Identify Clients**: Who uses this interface? What do they actually need?
2. **List Required Methods**: Only methods clients call; omit implementation details
3. **Check Cohesion**: Do all methods work toward the same goal? If not, split the interface
4. **Verify Minimal**: Can you remove any method without breaking clients? If yes, remove it
5. **Document Contracts**: What do methods guarantee? What can fail? Use structured comments
6. **Check Mutability**: Should some methods be on a separate "mutator" interface?
7. **Review Generics**: Do generic parameters complicate the contract? If yes, simplify
8. **Plan Evolution**: How will this interface change? Make room for extension without breaking

## Anti-Patterns

- Creating "fat" interfaces with 20 methods; forces clients to implement/mock unused methods (Interface Segregation violation)
- Mixing concerns (data access + transformation) in one interface; clients should pick the pieces they need
- Exposing implementation details in interface signatures (getInternalState() exposes architecture)
- Ignoring variadic or default arguments; they complicate the contract and hide complexity
- Not versioning interfaces; breaking changes ripple to all clients without warning
- Assuming interface will never change; design for extension, not rigidity

## Further Reading

- Robert C. Martin, _Clean Code_ and _Clean Architecture_, on interfaces
- Sandi Metz, _Practical Object-Oriented Design_, Chapter 5 (Writing Flexible Code)
- Gang of Four, _Design Patterns_, Chapter 2 (Design Principles)
