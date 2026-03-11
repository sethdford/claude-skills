---
name: review-checklist-design
description: Design effective review checklists that surface defects without slowing teams down. Use when creating domain-specific review criteria.
---

# Review Checklist Design

Create checklists that guide reviewers without creating busywork.

## Context

You are helping design review checklists for specific domains (backend services, frontend components, infrastructure, security). If you have code samples or known defect patterns, use them.

## Domain Context

- Toyota's andon cord system: checklists should surface problems _before_ they reach customers
- Cognitive science research: humans are poor at remembering checklists; automation is better than willpower
- High-performing teams (Forsgren et al., "Accelerate"): checklists enable distributed review without bottlenecks

Key principles:

1. **Automate what you can**: Linters, formatters, and CI gates handle style. Checklists should focus on judgment calls
2. **Domain-specific matters**: A backend service checklist differs from a frontend component checklist. Customize, don't reuse
3. **Checklists are teaching tools**: Each item should teach reviewers what to look for

## Instructions

1. **Identify defect categories**: Ask engineers "what defects did we miss in review?" Group by type (performance, security, logic, maintainability)
2. **For each category, write one checklist item**: Example: "Performance: does this query use indexes, or could it N+1?" not "Are queries efficient?"
3. **Add failure examples**: Each checklist item should have a 1-2 line example of what to catch
4. **Separate automation from judgment**:
   - Automation: "Linter passes" (no checklist item, just CI gate)
   - Judgment: "Considered error edge cases" (human reviewers ask this)
5. **Keep to 5-8 items**: Longer checklists are ignored. Focus on high-impact categories
6. **Link to standards**: Reference your code-review-standards for each item
7. **Iterate annually**: Track what defects escape review. Add checklist items for missed patterns

Example backend service checklist:

```
- [ ] Queries: no N+1 queries, uses appropriate indexes
- [ ] Errors: all error paths logged with context, not silently dropped
- [ ] Dependencies: no new external API calls without timeout/retry logic
- [ ] Data: no unencrypted sensitive data in logs or transit
- [ ] Backwards compatibility: API changes are versioned or have migration path
```

## Anti-Patterns

- **Checklists that automate should be removed**: If you have a checklist item "no console.log statements", that's a linter rule, not a review item. Automate it and remove the checklist item
- **Checklists that overwhelm**: LLMs sometimes create 20-item checklists that reviewers ignore. Focus on the 5 categories that catch 80% of defects
- **Checklists without context**: LLMs list criteria without explaining _why_. Each item needs a business reason (performance, security, maintainability) so reviewers understand its importance
- **Checklists that never evolve**: If a defect type stops showing up, remove that checklist item. If new defects emerge, add items. Stale checklists lose credibility

## Further Reading

- Gawande, Atul. "The Checklist Manifesto: How to Get Things Right." Metropolitan Books, 2009.
- Forsgren, Nicole et al. "Accelerate." IT Revolution Press, 2018. Chapter on practices that drive delivery.
- Raymond, Eric. "The Cathedral and the Bazaar." O'Reilly, 1999. On distributed code review
