---
name: error-handling-patterns
description: Strategies for handling errors: exceptions, error types, recovery strategies, and error propagation.
---

# Error Handling Patterns

Systematic approaches to error management that preserve debuggability and recovery.

## Context

You are helping the engineer design error handling. If code is provided, assess whether errors are explicit, catchable, and recoverable. Poor error handling is a hidden time bomb in production.

## Domain Context

- **Fail Fast, Fail Loud**: Don't swallow exceptions; propagate or handle explicitly
- **Specific Exceptions**: Throw specific exception types; generic Exception hides intent
- **Recovery Strategy**: Can the caller recover? If not, don't catch; let it propagate
- **Error Context**: Include relevant data in exceptions (user ID, operation, state)
- **Logging**: Log _why_ an error occurred, not just that it occurred

## Instructions

1. **Identify Error Boundaries**: Where can things fail? Network, parsing, database, arithmetic?
2. **Choose Exception Type**: Specific > generic; InvalidUserException > Exception
3. **Include Context**: Add user ID, operation, state to exception messages
4. **Plan Recovery**: If you catch an error, can you recover? If not, don't catch it
5. **Document Throws**: Declare checked exceptions or document unchecked ones
6. **Test Error Paths**: Write tests for error cases; normal cases hide error bugs
7. **Avoid Silent Failures**: Never catch and ignore; at minimum log
8. **Use Error Enums**: For recoverable errors, use Result<T, Error> or Either types

## Anti-Patterns

- Catching Exception and logging it, then continuing; the bug often recurs silently
- Generic exception handlers (catch Exception {...}) that hide specific failures; you can't debug what you don't see
- Throwing exception on non-exceptional flows (e.g., "User not found" as exception); exceptions are for errors, not control flow
- Losing error context in exception messages; "Error occurred" tells you nothing; include IDs, values, operations
- Not testing error paths; bugs in error handling code are the hardest to find in production
- Exceeding retry budgets; retrying forever on transient errors masks systemic problems
- Hiding errors in middleware; errors should bubble up with context, not be swallowed

## Further Reading

- Robert C. Martin, _Clean Code_, Chapter 7 (Error Handling)
- Joe Armstrong, _Programming Erlang_, Chapter 7 (Error Handling)
- John Ousterhout, _A Philosophy of Software Design_, on exceptions vs. error codes
