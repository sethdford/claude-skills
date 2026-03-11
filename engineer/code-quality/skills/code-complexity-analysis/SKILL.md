---
name: code-complexity-analysis
description: Measuring and reducing cyclomatic complexity and cognitive complexity to improve maintainability.
---

# Code Complexity Analysis

Quantifying and reducing the inherent difficulty of code.

## Context

You are helping the engineer measure and reduce code complexity. If code is provided, calculate metrics and suggest decomposition strategies. Complexity is a primary predictor of bugs.

## Domain Context

- **Cyclomatic Complexity**: Number of independent paths through code; each decision point adds 1
- **Cognitive Complexity**: How hard is it for a human to understand? Nesting, jumps, and abstractions add cost
- **Threshold**: Cyclomatic complexity > 10 is a smell; > 15 demands refactoring
- **Testing Cost**: Each decision path requires a test; high complexity means high test burden
- **Maintenance Cost**: High complexity → higher bug rate, slower changes

## Instructions

1. **Count Decisions**: Count if/else, switch, loops, operators; each adds 1 to cyclomatic complexity
2. **Check Nesting**: Each nested level adds cognitive cost; avoid nesting > 3 levels deep
3. **Identify Polymorphism Opportunities**: Replace switch/if chains with strategy pattern
4. **Extract Complex Conditions**: Move boolean logic to named methods or variables
5. **Break Long Methods**: Extract sub-methods even if called once; improves understanding
6. **Use Early Returns**: Guard clauses reduce nesting and improve readability
7. **Reduce Parameters**: Complex signatures add cognitive load; use parameter objects
8. **Test Complexity**: If > 10 tests needed for one method, it's too complex

## Anti-Patterns

- Dismissing complexity metrics as "not real"; high complexity correlates with bug density (empirically proven)
- Reducing complexity by extracting methods without naming them clearly; you just moved the complexity
- Creating single-responsibility methods that are still cognitively hard to understand; sometimes you need simpler logic
- Ignoring cyclomatic complexity because "the code works"; it works until the edge case you didn't test
- Using code golf or clever tricks to reduce line count; they increase cognitive complexity and invite bugs

## Further Reading

- Thomas J. McCabe, "A Complexity Measure" (1976, cyclomatic complexity)
- Sonar, Cognitive Complexity whitepaper
- John Ousterhout, _A Philosophy of Software Design_, on complexity
