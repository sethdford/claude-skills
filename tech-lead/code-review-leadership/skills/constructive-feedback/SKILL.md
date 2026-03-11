---
name: constructive-feedback
description: Provide code review feedback that improves code and team culture. Use when training reviewers or giving feedback guidelines.
---

# Constructive Code Review Feedback

Teach reviewers to give feedback that improves code, teaches, and builds team trust.

## Context

You are helping a tech lead establish feedback norms for code reviews. If you have examples of feedback that worked or feedback that caused friction, use them.

## Domain Context

- Brown et al. (Carnegie Mellon): constructive feedback improves outcomes 5x more than critical feedback alone
- Psychological safety research (Edmondson, "The Fearless Organization"): teams that trust reviewers take more risks and innovate more
- Google's engineering culture: code review feedback is about the code, never personal judgment

Key principles:

1. **Separate the code from the person**: "This code has a potential null pointer" not "You missed a null check"
2. **Assume good intent**: Authors try to do good work. Assume they didn't see a problem, didn't understand the requirement, or made a reasonable trade-off
3. **Explain the why**: "Simplify this loop" is vague. "This loop is O(n²); using a HashMap would be O(n)" is actionable

## Instructions

1. **Frame feedback as questions**: "Have you considered using a HashMap here instead?" invites discussion. "Use a HashMap" sounds dismissive
2. **Separate must-haves from nice-to-haves**: "This breaks the API contract (blocker)" vs. "Consider adding a comment explaining the heuristic (nice-to-have)"
3. **Provide examples**: If you suggest a change, show a 2-3 line example of what you mean
4. **Learn in public**: If you don't understand code, say so. "I'm not sure why you're doing X here—can you help me understand?" teaches and builds humility
5. **Celebrate good work**: Point out things you like. "Great use of the factory pattern here" takes 30 seconds and builds morale
6. **Know your team**: Different engineers need different feedback styles. Some prefer blunt; others prefer collaborative. Adjust
7. **Offer to pair**: For complex feedback, offer to pair program instead of writing 10 comments
8. **Model the feedback you want**: If you want kind, clear feedback, give kind, clear feedback

Example feedback:

```
Bad: "You're not handling the error case."
Good: "I notice this doesn't handle the case where the API returns a 500. Should we retry, or bubble the error to the caller?"

Bad: "This is inefficient."
Good: "This iterates the array twice; we could do it in one pass by tracking both min and max simultaneously. Want help refactoring?"

Bad: "You should use TypeScript."
Good: "Using TypeScript here would catch the type error I found. Not required, but worth considering for future work."
```

## Anti-Patterns

- **Feedback as teaching moments gone wrong**: LLMs sometimes use code review as a chance to teach best practices unprompted. Not every review is a teaching opportunity. Respect the author's context
- **Conflating personal style with correctness**: LLMs sometimes give feedback on tabs vs. spaces or naming preferences. Automate style, don't review it manually
- **Not explaining the business impact**: LLMs mention "this could be cleaner" without explaining why it matters. "Cleaner" is subjective. "This adds O(n) complexity for future readers" is objective and motivating
- **Feedback without empathy**: LLMs forget that receiving harsh feedback on code you spent hours on is demoralizing. Always assume good intent and show respect

## Further Reading

- Edmondson, Amy C. "The Fearless Organization: Creating Psychological Safety in the Workplace for Learning, Innovation, and Growth." Wiley, 2018.
- Stone, Douglas & Heen, Sheila. "Thanks for the Feedback: The Science and Art of Receiving Feedback Well." Viking, 2014.
- Brown, Brené. "Dare to Lead: Brave Work. Tough Conversations. Whole Hearts." Random House, 2018.
