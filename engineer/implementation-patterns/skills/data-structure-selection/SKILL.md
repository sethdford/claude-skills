---
name: data-structure-selection
description: Choosing optimal data structures based on access patterns and performance requirements.
---

# Data Structure Selection

Matching data structures to your performance requirements.

## Context

You are selecting data structures. Understand tradeoffs: access time, insertion, deletion, memory.

## Domain Context

- **Array**: O(1) random access; O(n) insertion
- **Linked List**: O(n) random access; O(1) insertion (if you have pointer)
- **Hash Table**: O(1) average access; O(n) worst case
- **Tree**: O(log n) balanced access; O(n) unbalanced
- **Heap**: O(1) min/max; O(log n) insertion

## Instructions

1. **Analyze Access Patterns**: Read-heavy? Write-heavy? Random access? Ordered?
2. **Identify Bottleneck**: Insertion? Lookup? Iteration?
3. **Compare Options**: List pros/cons of 2-3 structures
4. **Benchmark**: If unclear, measure with realistic data
5. **Choose**: Select structure with best worst-case for bottleneck
6. **Monitor**: Track performance; be ready to change if patterns shift

## Anti-Patterns

- Choosing structure based on familiarity not performance
- Not considering space overhead; 10x lookup speedup doesn't matter if memory explodes
- Using unbalanced trees; always use balanced (AVL, Red-Black, B-Tree)
- Ignoring cache locality; array beats linked list even with worse complexity
- Micro-optimizing data structures while algorithmic cost dominates

## Further Reading

- Donald Knuth, _The Art of Computer Programming_
- MIT OpenCourseWare, _Introduction to Algorithms_
