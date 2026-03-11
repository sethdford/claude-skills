---
name: system-decomposition
description: Break complex systems into bounded contexts with DDD. Map business capabilities to service boundaries, define ubiquitous language, assess cohesion/coupling. Use when refactoring monoliths or designing new architectures.
context: fork
agent: general-purpose
allowed-tools: Read, Grep, Glob, Write, Edit
---

# System Decomposition

Systematically decompose complex systems using Domain-Driven Design: identify business capabilities, define bounded contexts, evaluate cohesion/coupling, design integration patterns.

## Context

You are decomposing a system into services or modules. Your role is to:

- Map business capabilities (not technical layers)
- Define bounded contexts with explicit boundaries
- Establish ubiquitous language (shared vocabulary per context)
- Assess cohesion (focus) and coupling (dependencies)
- Design integration patterns (sync API vs async events)

Good decomposition follows business domains, not technology layers. Anti-pattern: UserService, OrderService, PaymentService (implementation detail names) instead of Auth Realm, Commerce Hub, Payment Platform (domain names).

## Domain Context

Based on Eric Evans' _Domain-Driven Design_ and Sam Newman's _Building Microservices_:

- **Bounded Context**: Explicit boundary around business capability. Each context has its own domain model.
- **Ubiquitous Language**: Shared vocabulary within context (Order, Customer, Invoice). Prevents translation errors.
- **Aggregate**: Entity cluster within context. Single consistency boundary. Example: Order + OrderItems as one aggregate.
- **Integration**: How contexts communicate (Sync via API, Async via events, Shared database)
- **Cohesion**: Does everything in the context serve one purpose?
- **Coupling**: How many other services must it call?

## When to Use This Skill

- Breaking monolith into services
- Designing new system architecture
- Refactoring tight coupling
- Aligning engineering teams to services
- Preparing for independent scaling/deployment

## Prerequisites

- Understand business domains and pain points
- Know current system architecture (if refactoring)
- Have stakeholders available to discuss domain
- Can draw diagrams (whiteboard, miro, draw.io)

## Instructions (Detailed)

### 1. **Identify Business Capabilities**

Ask: "What does the business do?"

Example (E-commerce):

- Authentication (who are you?)
- Commerce (what do you want?)
- Payment (how much does it cost?)
- Fulfillment (ship it)
- Analytics (understand customers)
- Support (help customers)

Each capability can become a bounded context.

### 2. **Define Bounded Contexts**

For each capability, establish boundary with explicit name and responsibilities.

**Example**:

```
Auth Realm (Authentication)
- User registration, login, session management
- Produces: authenticated identity tokens
- Language: User, Credential, Session, Auth Token

Commerce Hub (Order Processing)
- Order creation, cart management, inventory
- Consumes: Auth tokens
- Produces: Order events
- Language: Order, Customer, Product, Cart, OrderItem

Payment Platform (Payment Processing)
- Payment processing, refunds, accounting
- Consumes: Order events
- Produces: Payment status events
- Language: Payment, Invoice, Transaction, Settlement
```

### 3. **Map Ubiquitous Language**

Define key terms within each context:

```
Auth Realm:
- "User" = identity with credentials
- "Session" = authenticated connection

Commerce Hub:
- "Order" = customer purchase request
- "Customer" = entity that places orders (different from Auth's User)

Payment Platform:
- "Invoice" = billable entity (different from Order)
- "Settlement" = final accounting status
```

Contexts use same words differently. Clear boundaries prevent confusion.

### 4. **Assess Cohesion & Coupling**

**Cohesion** (within context):

- Do all functions serve one purpose? (high = good)
- Would we change them for the same business reason? (yes = high cohesion)

**Coupling** (between contexts):

- How many services must this call to complete a request?
- Sync vs Async: Sync = tight coupling, Async = loose coupling
- Target: Cohesion >80%, Coupling <3 sync calls/request

### 5. **Design Integration Patterns**

**Synchronous** (API call):

- Used for immediate results
- Tightly coupled
- Simple debugging
- Example: User creates order → Commerce Hub calls Payment Platform → charge card immediately

**Asynchronous** (event):

- Fire-and-forget
- Loosely coupled
- Difficult debugging
- Example: Order created → event published → Payment Platform subscribes and processes later

### 6. **Create Context Diagram**

Boxes = Contexts, Arrows = Synchronous calls, Events = Asynchronous communication.

```
┌──────────────┐        ┌──────────────┐        ┌──────────────┐
│  Auth Realm  │        │Commerce Hub  │        │   Payment    │
│              │        │              │        │  Platform    │
│ - Register   │──API───│ - Order      │───API──│ - Process    │
│ - Login      │        │   creation   │        │   payment    │
│ - Session    │        │ - Inventory  │        │ - Refund     │
└──────────────┘        │              │        └──────────────┘
                        │ Order Created│
                        │ Event ────────────────┐
                        └──────────────┘        │
                                        Event Handler
                                        (async payment)
```

### 7. **Verify Against Anti-Patterns**

- **Distributed monolith**: Services so tightly coupled they act as one → redraw boundaries
- **Service per table**: Data-driven decomposition (wrong) instead of domain-driven (right)
- **Chatty services**: Need >10 calls to complete request → larger bounded contexts
- **God context**: One service does everything → split into multiple contexts

## Output Format

When decomposing, deliver:

1. **Business Capabilities**: What the system does
2. **Bounded Contexts**: Explicit boundaries with names
3. **Context Diagram**: Visual showing contexts and integration
4. **Ubiquitous Language**: Key terms per context
5. **Integration Patterns**: Sync/Async by integration point
6. **Cohesion/Coupling Assessment**: Scores for each context
7. **Deployment Plan**: How to implement decomposition

## Worked Example

**Monolith**: Single "UserService" handling everything (100K lines)

**Issues**:

- Changes to UI tier require payment code changes
- Teams can't deploy independently
- Database contention

**Decomposition**:

```
Bounded Contexts:
1. Auth Realm: Registration, login, profiles
2. Commerce Hub: Orders, cart, inventory
3. Payment Platform: Payments, invoicing, settlements
4. Analytics: User behavior, metrics
```

**Cohesion Scores**:

- Auth Realm: 95% (all about identity)
- Commerce Hub: 85% (order-related, but inventory is borderline)
- Payment Platform: 90% (all about money)

**Coupling Analysis**:

- Commerce → Payment (sync): Payment::charge(amount)
- Order Created → Analytics (async): Event subscriber

**Integration**:

```
Commerce Hub: POST /payment/charge with Order details
Response: Payment ID + status
On failure: Rollback order

Analytics: Subscribes to "OrderCreated" event
No coupling: Order doesn't wait for analytics
```

## Decision Framework

- **One large context or many small?**: Start coarse; split when pain emerges
- **Sync or Async?**: Sync if needs immediate response (payment); Async if fire-and-forget (notifications)
- **Shared data or separate databases?**: Separate per context (independence); shared only for atomic transactions
- **Communication overhead?**: If sync calls >3 per request, reconsider boundaries

## Anti-Patterns

- **Premature Microservices**: Break before understanding domains
- **Technology-Driven**: "Python team" vs "Python-for-ML domain"
- **Ignoring Coupling**: Services talk to every other service
- **No Ubiquitous Language**: Same word means different things

## Quality Checklist

- [ ] Each context has single business responsibility
- [ ] Contexts named after domain (not tech: "Auth Realm" not "UserService")
- [ ] Ubiquitous language documented per context
- [ ] Cohesion >80% for each context
- [ ] Coupling <3 sync calls per request
- [ ] Integration patterns clear (sync/async)
- [ ] Deployment independence verified
- [ ] Teams can own individual contexts

## Further Reading

- Eric Evans, _Domain-Driven Design_ (2003) — Foundational
- Sam Newman, _Building Microservices_ (2nd ed., 2021) — Practical decomposition
- Dora et al., _Accelerate_ — Impact of decomposition on deployment frequency
