# Bug Investigation Report

## Bug Summary

[Concise description of the bug: what fails, how often, impact]

## Reproduction Steps

[Exact steps to make bug happen consistently]

## Data Gathered

- **Stack trace**: [Error with line numbers]
- **Logs**: [Relevant logs around failure]
- **System state**: [Memory, CPU, environment info]
- **Input**: [Data that triggers bug]

## Hypothesis #1

[Testable hypothesis about root cause]

### Experiment

[Minimal change to test hypothesis]

### Result

[What you found - confirmed, refuted, or inconclusive]

## Hypothesis #2 (if needed)

[Next hypothesis if first was refuted]

### Experiment

[Test for second hypothesis]

### Result

[What you found]

## Root Cause

[Why the bug actually happens - must explain all observations]

## Fix

[Code changes to address root cause]

```
[language]
[fixed code]
```

## Verification

- **Bug-triggering steps now work**: [Yes/No]
- **Edge cases tested**: [List cases tested]
- **No new bugs introduced**: [All tests pass/specific tests]

## Regression Test

[Test code preventing bug reappearance]

## Commit Message

```
fix: [concise description]
```
