---
name: review-culture-guide
description: Build a review culture where feedback improves code and team relationships. Use when establishing review norms and psychological safety.
---

# Review Culture Guide

Establish a culture where code review is trusted, fast, and a learning opportunity, not a gatekeeping exercise.

## Context

You are helping a tech lead shape team culture around code review. If you have team composition, maturity level, or current review dynamics, use them.

## Domain Context

- Psychological safety (Edmondson): teams with high trust submit riskier, more innovative code and improve faster
- High-performing teams (Forsgren et al.): review culture, not process, drives outcomes
- Research: culture that separates code criticism from personal criticism drives 3-5x faster learning

Key principles:

1. **Assume good intent**: Authors try to write good code. Reviewers try to improve it. Start with that premise
2. **Feedback is a gift**: Receiving feedback is how we improve. Creating a culture where engineers seek feedback (not avoid it) is the goal
3. **Psychological safety enables risk-taking**: Teams that fear harsh review write safe, boring code. Teams that trust reviews write innovative code

## Instructions

1. **Model good review behavior**: As a tech lead, demonstrate the feedback style you want to see. Write kind, clear, specific comments that focus on the code
2. **Celebrate reviews**: When someone gives great feedback, acknowledge it. "Thanks for the detailed review on the caching logic—that insight will help us scale"
3. **Celebrate learning from review**: When someone receives feedback and improves, acknowledge it. "Great catch in your own code review—you're building good review instincts"
4. **Make review a learning opportunity**: Pair junior engineers with senior reviewers. Have reviews become teaching moments
5. **Establish "review as gift" framing**: In team meetings, frame code review as "we help each other write better code" not "we catch mistakes"
6. **Normalize back-and-forth discussion**: Review should be a conversation. It's OK to disagree and discuss. Author should feel comfortable explaining their trade-offs
7. **Create safe space for "I don't understand"**: Reviewers should feel safe saying "I don't understand this logic—can you help me?" This often reveals unclear code
8. **Measure culture health**: Ask the team "do you feel safe receiving feedback?" and "do you feel your feedback is heard?" in retrospectives

Red flags (culture problems):

- Reviews feel like interrogations
- Authors feel blamed or attacked
- People submit safe, unambitious code to avoid criticism
- Same people do all reviews (gatekeeping, not teaching)
- Feedback is vague or personal ("this is bad" vs. "this doesn't handle the edge case")

Green flags (healthy culture):

- Authors thank reviewers for feedback
- Reviewers ask questions before rejecting code
- New engineers feel comfortable requesting reviews
- Disagreements are discussed as trade-offs, not right vs. wrong
- Review time is fast because feedback is clear and uncontroversial

## Anti-Patterns

- **Culture without systems**: LLMs sometimes recommend building a "positive review culture" without establishing systems (standards, checklists, automation) to enable it. Culture + systems work together
- **Assuming culture can be mandated**: You can't force culture. You can model it, incentivize it (recognize good reviews), and measure it (survey psychological safety), but ultimately it emerges over time
- **Confusing culture with process**: Process (standards, gates, tools) is not culture. Process without culture creates compliance; culture without process creates chaos. Need both
- **Ignoring power dynamics**: A tech lead giving harsh feedback has different impact than a peer. Be aware that seniority shapes how feedback lands

## Further Reading

- Edmondson, Amy C. "The Fearless Organization: Creating Psychological Safety in the Workplace for Learning, Innovation, and Growth." Wiley, 2018.
- Forsgren, Nicole et al. "Accelerate: Building and Scaling High Performing Technology Organizations." IT Revolution Press, 2018. Culture chapter.
- Brown, Brené. "Dare to Lead: Brave Work. Tough Conversations. Whole Hearts." Random House, 2018.
