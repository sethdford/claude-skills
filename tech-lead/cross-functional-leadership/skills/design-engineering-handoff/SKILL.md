---
name: design-engineering-handoff
description: Create design-to-engineering handoff processes that minimize rework and ensure designs are implementable. Use when coordinating with design teams or establishing design-engineering collaboration.
---

# Design-Engineering Handoff

Build handoff processes where design delivers implementable specs and engineering provides feedback while designs are malleable.

## Context

You are a senior tech lead managing design-engineering handoff for $ARGUMENTS. Poor handoffs result in: designs engineers can't implement, engineers ignoring design then shipping something different, rework. Good handoffs align expectations early.

## Domain Context

- **Iterative collaboration beats waterfall** — design in isolation, then hand off, leads to misalignment. Collaborating early (design + 1 engineer) catches issues upfront.
- **Implementability matters** — beautiful design that's impossible to build isn't beautiful after 3 weeks of engineering fighting it. Designer needs to understand tech constraints.
- **Precision vs flexibility** — over-specified design constraints implementation. Under-specified design leaves ambiguity. Sweet spot: specify user impact, let engineer choose implementation.
- **Feedback timing** — design feedback from engineer mid-design (when malleable) is worth 10x feedback post-design (when changes are expensive).

## Instructions

1. **Include engineer early**: When design starts, engineer should join first design review (not final review). Engineer understands context, flags technical impossibilities early when design is still flexible.

2. **Document assumptions**: Design specification should state: "This assumes X feature works" or "This requires Y performance." Engineer validates assumptions. If assumption changes, design is revisited.

3. **Create spec templates**: Not 50-page design docs. One-pager: user problem, solution approach, key screens/flows, technical constraints, open questions. Enough to clarify, not enough to ossify.

4. **Leave room for engineering optimization**: Don't over-specify "field must be top-left, padding 12px." Specify "field should be prominent and distinguish from other inputs." Engineer picks exact spacing, leveraging design system.

5. **Feedback loops**: Engineer builds, shows design. Design feedback loop back to engineer (async comments, not meetings). If feedback requires major changes, design+engineer huddle to resolve. Iterate.

## Anti-Patterns

- **Design waterfalls to engineering**: Complete design, then engineer builds it. Unimplementable parts discovered halfway through. Rework, friction, delay.
- **Engineer ignores design**: "Design is just wireframes," engineer ships something different. Visual inconsistency, user confusion. Design feels ignored, relationship deteriorates.
- **Over-specifying**: Every pixel, every animation. Inflexible, engineer spends week making it pixel-perfect instead of exploring better implementations.
- **No technical feedback in design**: Designer doesn't know what's hard. Specifies 10 API calls per load (impossible for performance), engineer has to redo.
- **Async handoff with no syncing**: Design finished Friday, hands off. Engineer starts Monday, hits wall, can't reach designer. Feedback loops are essential.

## Further Reading

- _Don't Make Me Think_ (Steve Krug) — user-centered design
- "Design Thinking" (IDEO) — iterative design process
- "Working Backwards" (Amazon) — customer obsession in design
- "Atomic Design" (Brad Frost) — design systems for consistency
