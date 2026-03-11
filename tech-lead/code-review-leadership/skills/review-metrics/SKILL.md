---
name: review-metrics
description: Track code review health metrics (cycle time, review participation, defect escape) to improve review process. Use when analyzing review effectiveness.
---

# Review Metrics

Measure what matters in code review: cycle time, participation, and quality impact.

## Context

You are helping a tech lead monitor code review health. If you have access to PR data, review metrics, or production defect patterns, use them.

## Domain Context

- DORA metrics (Forsgren et al., "Accelerate"): lead time for changes and deployment frequency are strong indicators of team health
- GitHub data: median review time for high-performing teams is 24 hours; > 48 hours signals a bottleneck
- Studies show review cycle time matters more than review depth for shipping quality

Key principles:

1. **Lead time is the key metric**: Time from PR open to merge strongly correlates with team velocity and morale
2. **Participation diversity matters**: If only 1-2 people review code, you have a bottleneck and knowledge loss
3. **Defect escape rate measures actual quality**: Review metrics (coverage, comments) don't matter if defects still reach production

## Instructions

1. **Track lead time**: Measure time from PR open to merge. Target: < 24 hours. Alert if > 48 hours for > 20% of PRs
2. **Track review participation**: What % of PRs are reviewed by at least 2 people? Target: 80%+. Healthy sign of knowledge sharing
3. **Track review cycle time**: Time from PR submitted to first review comment. Target: < 4 hours. If > 8 hours, you have a bottleneck
4. **Track reviewer diversity**: How many unique reviewers reviewed PRs last month? If < 3 people reviewed 80%+ of PRs, knowledge is concentrated
5. **Track comment count**: Average comments per PR. High comments (> 15) might signal unclear standards or unproductive feedback
6. **Track defect escape**: What % of defects in production came from code that was reviewed? If > 20%, review standards need adjustment
7. **Correlate to outcomes**: When you change review standards or process, re-measure. Did lead time improve? Did defects increase?

Example dashboard:

```
Metric | Target | Current | Status
─────────────────────────────────
Lead Time | < 24h | 31h | ⚠ (too slow)
Median Review Cycle | < 4h | 6h | ⚠ (bottleneck)
Reviewer Diversity | 3+ | 5 | ✓
Defect Escape Rate | < 20% | 18% | ✓
PRs in Review | < 5 | 12 | ⚠ (backlog building)
```

## Anti-Patterns

- **Optimizing wrong metrics**: LLMs sometimes recommend tracking "comments per PR" as a quality metric. More comments don't mean higher quality. Focus on lead time and defect escape
- **Metrics without context**: "Review time is 2 days" is meaningless without understanding why (team size, complexity, part-time reviewers). Always dig into context
- **Gaming metrics**: If you measure "time to first review," developers will submit incomplete PRs early. Measure what you care about (quality + speed), not just one dimension
- **No action from metrics**: Collecting metrics without improving based on them is pointless. If a metric goes red, investigate and improve

## Further Reading

- Forsgren, Nicole et al. "Accelerate: Building and Scaling High Performing Technology Organizations." IT Revolution Press, 2018.
- Kim, Gene et al. "The DevOps Handbook." IT Revolution Press, 2016. Chapter on metrics that matter.
- Humble, Jez & Farley, David. "Continuous Delivery." Addison-Wesley, 2010. Chapter on deployment pipeline metrics.
