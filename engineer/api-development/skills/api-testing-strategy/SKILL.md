---
name: api-testing-strategy
description: Contract testing, API mocking, integration testing, and end-to-end API testing.
---

# API Testing Strategy

Ensuring API reliability through comprehensive testing.

## Context

You are planning API tests. Use contract tests, mocking, and integration tests.

## Domain Context

- **Contract Testing**: Verify client/server agree on contract
- **Mocking**: Mock external dependencies for isolation
- **Integration**: Real server + real dependencies
- **Load Testing**: Can server handle expected load?
- **Chaos**: What happens when dependencies fail?

## Instructions

1. **Contract Tests**: Verify request/response schemas match
2. **Happy Path**: Normal operation; typical requests
3. **Error Cases**: All documented error codes; clients handle them
4. **Edge Cases**: Empty results, large responses, slow responses
5. **Integration**: Real dependencies; test flows
6. **Load**: Can server handle peak load?
7. **Chaos**: What if database is slow? Cache fails? Network partitions?

## Anti-Patterns

- Only happy path tests; miss most failure modes
- No contract tests; server and client drift
- Integration tests on real production data; pollution risk
- No load testing; surprises in production
- Not testing error paths; clients don't handle errors gracefully

## Further Reading

- Martin Fowler, _Contract Testing_
- Google Cloud API Testing best practices
- Chaos Engineering principles
