---
name: algorithm-analysis
description: Big O notation, time/space complexity analysis, and choosing efficient algorithms.
---

# Algorithm Analysis

Understanding and predicting algorithm performance.

## Context

You are analyzing algorithm complexity. Use Big O to compare approaches.

## Domain Context

- **Big O**: Worst-case growth rate; O(1), O(log n), O(n), O(n log n), O(n²)
- **Time vs. Space**: Tradeoff; faster algorithms often use more memory
- **Constant Factors**: O(n) with big constant might lose to O(n log n); measure
- **Practical**: Asymptotic analysis is useful; real data matters too

## Instructions

1. **Count Operations**: How many steps for input size n?
2. **Dominant Term**: n² + n → O(n²); drop constants and lower terms
3. **Compare Algorithms**: Which has better complexity for your problem?
4. **Consider Constants**: O(n) with big constant might lose to O(n log n)
5. **Measure**: Implement both; benchmark with real data
6. **Choose**: Pick algorithm with best complexity on expected input sizes

## Anti-Patterns

- Obsessing over Big O without measuring; constant factors matter
- Choosing O(n log n) over O(n) without analyzing input distribution
- Not considering space complexity; time-space tradeoffs exist
- Assuming theoretical optimum is practical; real implementation matters
- Ignoring cache effects; access patterns beat asymptotic analysis

## Further Reading

- Donald Knuth, _TAOCP_, Vol 1-3
- MIT OpenCourseWare, _Introduction to Algorithms_
