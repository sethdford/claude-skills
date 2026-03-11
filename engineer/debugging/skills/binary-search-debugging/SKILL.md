---
name: binary-search-debugging
description: Using bisect/git bisect to isolate failure to exact commit or code path.
---

# Binary Search Debugging

Efficiently narrowing problem scope through bisection.

## Context

You are using binary search to isolate a failure. Works for bugs and regressions.

## Domain Context

- **Git Bisect**: Half the commits; does bug exist here? Repeat until you find the culprit commit
- **Code Path**: Disable half the code; does bug reproduce? Narrow to affected code
- **Data Range**: Bugs with specific input; binary search the input space
- **Time Range**: Regression over time; binary search commits

## Instructions

1. **Identify Good and Bad Commits**: When did it work? When did it break?
2. **Run Git Bisect**: Automates binary search through commits
3. **Test at Bisect Point**: Does bug exist at this commit?
4. **Bisect Reports**: It, narrows range automatically
5. **Find Exact Commit**: Run to completion; identifies culprit
6. **Review Commit**: What changed? Why does it cause the bug?
7. **Code Path Bisect**: Disable features/code paths; find what triggers bug

## Anti-Patterns

- Assuming recent commit caused it; test assumptions with bisect
- Not using bisect on large commit ranges; manual search is slow
- Bisecting without reproducible test; need consistent yes/no answer
- Not reviewing found commit; understanding the bug matters

## Further Reading

- Git bisect documentation
- Linux kernel debugging; git bisect is standard there
