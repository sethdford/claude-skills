---
name: test-strategy
description: Create testing pyramid with unit/integration/E2E strategy. Define coverage targets and high-risk testing. Use when planning tests for features.
context: fork
agent: general-purpose
allowed-tools: Read, Grep, Glob, Write, Edit, Bash
---

# Test Strategy

Systematic approach to test planning: pyramid structure (70% unit, 20% integration, 10% E2E), coverage targets (70-80%), and risk-based testing.

## Context

You are planning test coverage for a feature. Your role is to:

- Design test pyramid: unit (fast, isolated) > integration (slower, real) > E2E (slowest, brittle)
- Identify high-risk code needing extra testing
- Set realistic coverage targets
- Balance speed (fast feedback) vs confidence (comprehensive testing)
- Avoid the "test everything" trap

Good testing builds confidence, not false security. 100% coverage often means testing trivia instead of business logic.

## Domain Context

Based on Martin Fowler, Google Testing, and J.B. Rainsberger:

- **Test Pyramid**: Most tests at bottom (unit), fewer at middle (integration), few at top (E2E)
- **Coverage Target**: 70-80% code coverage sufficient; 100% is waste
- **Business Value**: Test what users care about; not every code path
- **High-Risk Code**: Auth, payment, data integrity → extra testing
- **Speed**: Unit tests <100ms; integration <1s; E2E <10s each

## When to Use This Skill

- Planning tests for a new feature
- Adding tests to existing codebase
- Auditing test coverage (too little or too much)
- Improving test speed (too slow)
- Preparing for high-risk deployments

## Prerequisites

- Understand feature requirements and acceptance criteria
- Know the domain (what's valuable to test vs trivial)
- Have testing tools/frameworks available
- Can run tests locally in <5 seconds

## Instructions (Detailed)

### 1. **Define Layers**

**Unit Tests** (70% of tests):

- Single function/method in isolation
- Mock external dependencies
- Run in <1ms each
- Example: `test_calculate_discount_rate_returns_0_05_for_vip()`

**Integration Tests** (20% of tests):

- Component interaction with real dependencies
- Database, file system, real (test) services
- Run in <1s each
- Example: `test_user_registration_saves_to_database()`

**E2E Tests** (10% of tests):

- Full flow through system (UI → API → database)
- Real browser/client, real servers
- Run in <10s each
- Example: `test_checkout_flow_creates_order_and_sends_confirmation()`

### 2. **Identify High-Risk Code**

Ask: "What breaks the business?"

**High-risk areas**:

- **Authentication/Authorization**: Wrong user gets access
- **Payment Processing**: Charges wrong amount or double-charges
- **Data Integrity**: Corrupt or lost data
- **Critical Flows**: Core business logic
- **Security**: SQL injection, XSS, secrets leaked

**Low-risk areas**:

- Formatting (display logic)
- Trivial getters/setters
- Framework boilerplate
- Error messages (non-security)

### 3. **Set Coverage Target**

**Realistic targets**:

- High-risk code: 90%+ coverage
- Core logic: 80%+ coverage
- General code: 70-80% coverage
- Framework code: 50% coverage (don't over-test)

**Total target**: 70-80% for whole codebase.

Don't chase 100%. Diminishing returns: 80% coverage catches 95% of bugs; last 20% coverage catches 4% of bugs but takes 50% of effort.

### 4. **Plan Unit Tests**

For each function/method:

- **Happy path**: Normal input, expected output
- **Edge cases**: Boundary values (0, 1, -1, max, min)
- **Error cases**: Invalid input, exceptions

Example (Order::apply_discount):

- Happy path: valid discount code → correct reduction
- Edge case: discount = 100% → total = $0
- Error case: invalid code → raises exception

### 5. **Plan Integration Tests**

For each business flow:

- **Happy path**: Complete flow succeeds
- **Dependency failure**: Database down, service timeout
- **Data consistency**: Changes persist correctly

Example (User registration):

- Happy path: register → user saved → email sent
- Database failure: registration fails gracefully
- Duplicate email: rejected with clear error

### 6. **Plan E2E Tests**

For critical user journeys only:

- **Checkout flow**: Add to cart → checkout → payment → confirmation
- **Login flow**: Enter credentials → authorize → redirect to dashboard
- **Report generation**: Select criteria → generate → download

Avoid: Every button click, every error message, every combination. E2E tests are brittle and slow.

### 7. **Define Test Data Strategy**

- **Fixtures**: Reusable test data (predefined users, products)
- **Factories**: Generate test data on-the-fly
- **Mocks**: Fake dependencies
- **Test Databases**: Real database with test schema

### 8. **Document Coverage Goals**

Create a matrix showing coverage targets:

| Area               | Unit | Integration | E2E | Coverage Target |
| ------------------ | ---- | ----------- | --- | --------------- |
| User registration  | 10   | 3           | 1   | 90%             |
| Payment processing | 15   | 5           | 1   | 95%             |
| Reporting          | 5    | 2           | 1   | 70%             |

## Output Format

When planning tests, deliver:

1. **Test Pyramid**: Counts for unit/integration/E2E
2. **Coverage Targets**: By risk area
3. **Unit Test Plan**: What functions, what cases
4. **Integration Test Plan**: What flows, what dependencies
5. **E2E Test Plan**: Which user journeys
6. **Test Data**: How to set up test data
7. **Success Criteria**: What passing tests prove

## Worked Example: E-Commerce Order Feature

**Feature**: Users can create orders with discount codes, apply taxes, and process payments.

### Test Pyramid

```
E2E (10%): 2 tests
- Checkout flow end-to-end
- Order with discount code

Integration (20%): 8 tests
- Order creation saves to DB
- Payment gateway integration
- Email notifications sent

Unit (70%): 28 tests
- Discount calculation
- Tax calculation
- Validation (email, quantity, amount)
- Payment amount calculation
```

### Coverage Targets

| Area                | Target | Rationale                    |
| ------------------- | ------ | ---------------------------- |
| Discount logic      | 95%    | High-risk: affects revenue   |
| Tax logic           | 90%    | High-risk: affects revenue   |
| Payment integration | 95%    | High-risk: money involved    |
| Order persistence   | 85%    | Medium-risk: data integrity  |
| Email notifications | 60%    | Low-risk: cosmetic           |
| Error handling      | 80%    | Medium-risk: user experience |

**Overall target**: 80% code coverage

### Unit Tests (28 tests)

**Discount Calculation**:

- `test_calculate_discount_returns_0_05_for_vip_code()`
- `test_calculate_discount_returns_0_10_for_premium_code()`
- `test_calculate_discount_raises_for_invalid_code()`
- `test_calculate_discount_returns_0_for_no_code()`
- `test_calculate_discount_handles_max_discount()`

**Tax Calculation**:

- `test_calculate_tax_returns_correct_rate()`
- `test_calculate_tax_zero_for_tax_exempt_item()`
- `test_calculate_tax_accumulates_for_multiple_items()`
- `test_calculate_tax_rounds_correctly()`

**Validation**:

- `test_validate_email_rejects_invalid_format()`
- `test_validate_quantity_rejects_zero()`
- `test_validate_quantity_rejects_negative()`
- `test_validate_amount_rejects_zero()`
- `test_validate_amount_rejects_negative()`

...13 more unit tests

### Integration Tests (8 tests)

- `test_create_order_saves_to_database()`
- `test_order_persistence_retrieves_correct_data()`
- `test_payment_gateway_processes_valid_payment()`
- `test_payment_gateway_rejects_invalid_card()`
- `test_payment_failure_rolls_back_order()`
- `test_email_service_sends_order_confirmation()`
- `test_email_service_sends_payment_receipt()`
- `test_concurrent_orders_dont_interfere()`

### E2E Tests (2 tests)

- `test_complete_checkout_flow()` — Cart → Payment → Confirmation
- `test_checkout_with_discount_code()` — Apply code → discounted price → success

## Decision Framework

- **If mutation score is low**: Add more unit tests (logic isn't well-tested)
- **If tests are slow**: Move integration tests to unit (mock dependencies)
- **If coverage is >85%**: Stop chasing coverage; focus on risk-based testing
- **If feature touches payment/auth**: Increase coverage to 90%+
- **If flaky tests**: Too much E2E; move to integration/unit tests

## Anti-Patterns

- **100% Coverage Goal**: Wastes effort on trivial code; stops finding real bugs
- **Only E2E Tests**: Slow, brittle, hard to debug. Prefer unit tests
- **Testing Implementation, Not Behavior**: Tests break when refactoring, not when behavior changes
- **No High-Risk Focus**: Spend effort on what matters (payments, auth); less on formatting
- **Massive Test Data Setup**: Tests should be self-contained; use factories
- **Ignoring Flakiness**: Flaky tests are worse than none (erode trust)

## Quality Checklist

- [ ] Pyramid structure: 70% unit, 20% integration, 10% E2E
- [ ] Coverage targets: 70-80% overall, 90%+ for high-risk
- [ ] High-risk code identified (auth, payment, data)
- [ ] Each layer tested: happy path + edge cases + errors
- [ ] Tests are deterministic (no flakiness)
- [ ] Test data is repeatable and isolated
- [ ] Tests document expected behavior
- [ ] Performance: unit <100ms, integration <1s, E2E <10s
- [ ] No over-testing of trivial code
- [ ] Success criteria defined (what passing tests prove)

## Further Reading

- Martin Fowler, _Test Pyramid_ (blog post)
- J.B. Rainsberger, _Integrated Tests Are a Scam_ (conference talk)
- Google, _Testing on the Toilet_ (testing best practices)
- Kent Beck, _Test-Driven Development: By Example_
- Roy Osherove, _The Art of Software Testing_
