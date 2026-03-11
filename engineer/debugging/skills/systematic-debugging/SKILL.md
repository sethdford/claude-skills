---
name: systematic-debugging
description: Disciplined methodology to isolate bugs through hypothesis-driven testing. Form hypotheses, test them with minimal changes, narrow scope systematically. Use when bugs are unclear or reproduce intermittently.
context: fork
agent: general-purpose
allowed-tools: Read, Grep, Glob, Write, Edit, Bash
---

# Systematic Debugging

Disciplined approach to finding root cause by treating debugging as a scientific investigation, not a guessing game.

## Context

You are guiding systematic bug investigation. Your role is to:

- Help formulate clear, testable hypotheses about the failure
- Design minimal experiments to test each hypothesis
- Eliminate impossible causes systematically
- Narrow the problem space with each iteration
- Document findings to prevent regression

Debugging is hypothesis-driven experimentation, not random code inspection or prayer-driven programming.

## Domain Context

Based on Zeller's _Why Programs Fail_ and Robert C. Martin's discipline of debugging:

- **Reproducibility**: If you can't reproduce the bug consistently, it's a ghost. Spend time here.
- **Isolation**: What conditions trigger it? Code path, specific data, timing, environment?
- **Hypothesis**: What do you think went wrong? Must be falsifiable (testable).
- **Experiment Design**: Minimal change to test hypothesis. Change one thing at a time.
- **Iteration**: Each failed hypothesis narrows the search space. No progress = reassess assumptions.
- **Root Cause vs Symptom**: Fix the root cause, not the symptom. Symptoms can hide real problems.
- **Debugger > Print Statements**: Debuggers let you inspect state at breakpoints. Prints are for logging, not debugging.

## When to Use This Skill

- Bug is reported but you can't reproduce it yet
- Bug reproduced but root cause is unclear
- Bug has been "fixed" multiple times but keeps appearing (symptom-fixing)
- Bug is intermittent or timing-dependent
- Bug affects multiple systems and cause is uncertain
- Post-mortem: understanding why a bug happened to prevent recurrence

## Prerequisites

Before systematic debugging:

- **Read the Error Message**: Carefully. It often points to the real issue.
- **Check Git History**: When did this start? What changed?
- **Understand the Feature**: How is the code supposed to work?
- **Reproduce Locally**: If possible, get the bug to happen on your machine with minimal setup
- **Isolate Variables**: Can you narrow it down to a specific input, code path, or environment?

## Instructions (Detailed)

### 1. **Reproduce the Bug Consistently**

This is 80% of debugging. If you can't reproduce it, you can't debug it.

**Approach**:

- Get exact steps: "Click button X, fill field Y, click submit"
- Record inputs: The exact data that triggers the bug
- Record environment: OS, browser, version, dependencies
- Record timing: Does it happen immediately or after delay?
- Try to make it fail every time

**Example**:

```
Bug: Payment processing fails intermittently
Steps to reproduce:
1. Create order with 3+ items
2. Apply discount code "SAVE10"
3. Click "Process Payment"
4. Observe: 50% of time, get "Transaction timeout error"
```

If you achieve 100% reproduction, you're done with Step 1. If it's still intermittent, explore:

- Race conditions (timing)
- Concurrency issues (multiple requests)
- Environment-specific problems (network, database)
- Data-specific problems (certain inputs always fail)

### 2. **Gather Data at Failure Time**

Collect evidence:

- **Stack trace**: Full error with line numbers
- **Logs**: Application logs around failure time
- **System state**: Memory, CPU, disk at failure
- **Network traces**: If network-involved
- **Database state**: What data was in the database?
- **Request/response**: What input triggered the failure?

**Tools**:

- Debugger breakpoints to inspect variables
- Application logs (log level: DEBUG or TRACE for this area)
- Network inspector (browser DevTools or Wireshark)
- Database queries (EXPLAIN plans, slow query logs)
- System profiling (strace, ltrace, perf for C code)

**Example output**:

```
Stack trace:
TypeError: Cannot read property 'apply_discount' of undefined
  at PaymentProcessor.js:42 (apply_discount())
  at Order.js:88 (process())

Logs:
[2026-03-11 14:23:45] INFO: Order created, id=12345
[2026-03-11 14:23:46] DEBUG: Discount code "SAVE10" applied
[2026-03-11 14:23:47] ERROR: Cannot read property 'apply_discount' of undefined

Database state at failure:
SELECT * FROM orders WHERE id=12345;
id | discount_code | processed_at
12345 | SAVE10 | NULL

Request:
POST /orders/12345/process
Content-Type: application/json
{ "payment_method": "credit_card" }
```

### 3. **Form a Hypothesis**

Based on the data, make a testable guess:

**Bad hypotheses** (not falsifiable):

- "The code is broken"
- "Concurrency issue"
- "Network problem"

**Good hypotheses** (falsifiable, specific):

- "The discount object is undefined when `apply_discount()` is called"
- "The discount code is not being set correctly in the Order object"
- "The payment processing function expects discount to be a float, but it's receiving a string"

**Hypothesis template**:

> "If [condition], then [observable result]. When I check [specific place], I expect to find [specific data]."

**Example**:

> "If the discount code is not being parsed correctly, then the discount_rate variable should be undefined or have an unexpected value. When I inspect the Order object in the debugger after applying discount code, I expect discount_rate to be undefined."

### 4. **Design a Minimal Experiment**

Test the hypothesis with the smallest possible change:

**Before** (hypothesis: discount_rate is undefined):

```python
# Suspected code in order.py
def apply_discount(self, code):
    discount_rate = DISCOUNT_CODES.get(code)  # What if code is wrong?
    self.subtotal *= (1 - discount_rate)
```

**Experiment 1** (check hypothesis):

```python
# Add logging to inspect state
def apply_discount(self, code):
    discount_rate = DISCOUNT_CODES.get(code)
    print(f"DEBUG: code={code}, discount_rate={discount_rate}")  # Minimal change
    self.subtotal *= (1 - discount_rate)
```

Run with same inputs that triggered bug. If output shows `discount_rate=None`, hypothesis confirmed.

**Experiment 2** (test if that's the cause):

```python
# Fix the problem
def apply_discount(self, code):
    discount_rate = DISCOUNT_CODES.get(code, 0)  # Default to 0 if not found
    self.subtotal *= (1 - discount_rate)
```

Run same inputs. Does bug disappear?

### 5. **Execute Experiment and Evaluate**

Run the experiment:

```bash
# Original code with bug-triggering input
python order_processor.py --order-id 12345 --discount "SAVE10"

# Output:
# DEBUG: code=SAVE10, discount_rate=None
# TypeError: unsupported operand type(s) for *: 'float' and 'NoneType'
```

**Evaluation**:

- Hypothesis **confirmed**: discount_rate is None
- Root cause: DISCOUNT_CODES.get(code) returns None when code is not found
- Solution: Provide a default value or validate code before use

### 6. **Iterate if Hypothesis is Wrong**

If experiment shows something unexpected:

**Experiment result**: `discount_rate=0.1` (correctly found!)

**Conclusion**: discount_rate is NOT the problem. Hypothesis was wrong.

**New hypothesis**: Maybe `self.subtotal` is undefined?

```python
def apply_discount(self, code):
    discount_rate = DISCOUNT_CODES.get(code, 0)
    print(f"DEBUG: subtotal={self.subtotal}, discount_rate={discount_rate}")  # Check subtotal
    self.subtotal *= (1 - discount_rate)
```

Run again. If output shows `subtotal=None`, hypothesis 2 is confirmed. If subtotal is correct, form hypothesis 3.

**Keep narrowing**: Each failed hypothesis eliminates possibilities and narrows the search space.

### 7. **Verify Fix Resolves Issue**

Once root cause is found, implement the fix:

```python
# Before (buggy)
def apply_discount(self, code):
    discount_rate = DISCOUNT_CODES.get(code)  # Returns None if not found
    self.subtotal *= (1 - discount_rate)  # TypeError if discount_rate is None

# After (fixed)
def apply_discount(self, code):
    if code not in DISCOUNT_CODES:
        raise ValueError(f"Invalid discount code: {code}")
    discount_rate = DISCOUNT_CODES[code]
    self.subtotal *= (1 - discount_rate)
```

**Verify**:

- Bug-triggering input now fails with clear error (ValueError) instead of TypeError
- Invalid code is caught early, not late
- Valid codes still work correctly

### 8. **Write Test to Prevent Regression**

Ensure the bug doesn't reappear:

```python
def test_apply_discount_raises_on_invalid_code():
    order = Order(subtotal=100.00)
    with pytest.raises(ValueError, match="Invalid discount code"):
        order.apply_discount("INVALID_CODE")

def test_apply_discount_reduces_subtotal():
    order = Order(subtotal=100.00)
    order.apply_discount("SAVE10")  # 10% off
    assert order.subtotal == 90.00
```

Run tests. Both pass. Bug is fixed and regression-tested.

## Output Format

When using this skill, deliver:

1. **Bug Summary**: What was reported?
2. **Reproduction Steps**: How to make it happen
3. **Hypothesis**: What you think went wrong
4. **Experiment**: Minimal test to verify hypothesis
5. **Result**: What you found
6. **Root Cause**: Why the bug happened
7. **Fix**: Code changes to address root cause
8. **Verification**: Tests proving bug is fixed
9. **Commit**: Commit message with bug fix

Example output:

```
## Bug: Payment processing fails intermittently

### Reproduction
Steps: Create order, apply discount "SAVE10", process payment

### Hypothesis
Discount code parsing is broken; discount_rate is undefined.

### Experiment
Add debug logging to apply_discount() to inspect state:
[code showing experiment]

### Result
discount_rate=None when code is "SAVE10"

### Root Cause
DISCOUNT_CODES.get(code) returns None if code not found.
apply_discount() doesn't handle None.

### Fix
[fixed code]

### Verification
[tests passing]

### Commit
fix: handle invalid discount codes in apply_discount
```

## Worked Example: Intermittent Payment Timeout

**Bug Report**: "Payment processing times out randomly. Sometimes it works, sometimes it doesn't."

**Step 1: Reproduce**

Try 10 times with same input:

```
Attempt 1: Success (2.3s)
Attempt 2: Timeout (30s)
Attempt 3: Success (2.1s)
Attempt 4: Timeout (30s)
Attempt 5: Success (2.4s)
```

**Observation**: ~50% failure rate. Timing suggests either:

- Asynchronous operation not completing
- Race condition
- Load-dependent (slower under load)

**Step 2: Gather Data**

Logs during successful attempt:

```
[14:23:45.123] DEBUG: PaymentProcessor.process() called
[14:23:45.234] DEBUG: Contacting payment gateway...
[14:23:45.456] DEBUG: Gateway response received
[14:23:45.567] INFO: Payment processed successfully
```

Logs during timeout:

```
[14:24:01.123] DEBUG: PaymentProcessor.process() called
[14:24:01.234] DEBUG: Contacting payment gateway...
[14:24:31.456] ERROR: Timeout waiting for gateway response
```

**Observation**: Gateway response is sometimes slow (>30 seconds). Timeout is set to 30 seconds.

**Step 3: Form Hypothesis**

> "If the payment gateway is slow, the timeout will trigger. When I check the gateway response time, I expect it to sometimes exceed 30 seconds."

**Step 4: Design Experiment**

Add instrumentation to measure gateway response time:

```python
def process_payment(self, order):
    start_time = time.time()
    response = self.gateway.request(order)  # Might be slow
    elapsed = time.time() - start_time
    self.logger.info(f"Gateway response time: {elapsed:.2f}s")

    if elapsed > 25:  # Warn if close to timeout
        self.logger.warning(f"Slow gateway response: {elapsed:.2f}s")

    return response
```

**Step 5: Execute & Evaluate**

Run 10 times, collect data:

```
[14:25:01] Gateway response time: 2.34s
[14:25:02] Gateway response time: 28.56s ← Close to timeout!
[14:25:03] Gateway response time: 2.12s
[14:25:04] Gateway response time: 31.23s ← Timeout! (>30s)
[14:25:05] Gateway response time: 2.45s
```

**Conclusion**: Gateway is slow sometimes (2-30+ seconds). Current timeout of 30s is too tight.

**Step 6: Root Cause**

Payment gateway has variable latency (SLA is "up to 30 seconds"). Our timeout of 30 seconds is too aggressive; network jitter causes timeouts.

**Step 7: Fix**

Increase timeout and add retry logic:

```python
class PaymentGateway:
    TIMEOUT = 45  # Was 30; increased to 45s
    MAX_RETRIES = 3

def process_payment_with_retry(self, order):
    for attempt in range(self.MAX_RETRIES):
        try:
            return self.process_payment(order)
        except TimeoutError:
            self.logger.warning(f"Attempt {attempt+1} timed out, retrying...")
            time.sleep(2 ** attempt)  # Exponential backoff
    raise TimeoutError("Payment gateway unreachable after 3 attempts")
```

**Step 8: Verify**

Run 10 attempts:

```
✓ All 10 successful
Response times: 2.3s, 28.5s, 2.1s, 45.2s (retry 1) → success, 2.4s, ...
```

Success! No more timeouts.

**Step 9: Test**

```python
def test_payment_retries_on_timeout():
    gateway = MockGateway(responses=[
        TimeoutError(),  # Attempt 1 fails
        TimeoutError(),  # Attempt 2 fails
        {"status": "success"}  # Attempt 3 succeeds
    ])
    processor = PaymentProcessor(gateway)
    result = processor.process_payment_with_retry(order)
    assert result["status"] == "success"
```

**Commit**:

```
fix: increase payment gateway timeout and add retry logic

Payment gateway has variable latency (up to 30s). Previous timeout of 30s
was too aggressive; network jitter caused intermittent failures.

Changes:
- Increase timeout from 30s to 45s
- Add exponential backoff retry (max 3 attempts)
- Log retry attempts for monitoring

Fixes intermittent payment processing timeouts.
Verified: 10 consecutive successful payment attempts.
```

## Decision Framework

When debugging, use these decisions:

- **Can't reproduce?**: Investigate intermittency first (timing, data, environment). Don't proceed without reproduction.
- **Multiple hypotheses?**: Test the simplest/most likely first. Occam's Razor applies.
- **Hypothesis too complex?**: Break into smaller, falsifiable parts.
- **Many possible causes?**: Eliminate the simplest ones first (typos, off-by-one, None checks).
- **Fix causes new bugs?**: You fixed the symptom, not the root. Go back to root cause analysis.
- **Debugging > Printing**: Use a debugger to set breakpoints and inspect state. Print statements are for logging.
- **Still stuck after 1 hour?**: Take a break. Fresh perspective often reveals what you missed.

## Anti-Patterns (Expanded)

### 1. **Spray-and-Pray Debugging**

**Mistake**: Make random changes hoping one fixes it.

**Why LLMs make this**: Code generation is fast; testing changes feels like progress.

**Guard**: Form hypothesis first. Change one thing. Test. Evaluate. Repeat.

**Example**:

- Bad: Add null checks everywhere, logging everywhere, try different timeouts
- Good: Form hypothesis → minimal test → evaluate → fix root cause

---

### 2. **Debugging by Print Statements Only**

**Mistake**: Rely solely on logs; never use a debugger.

**Why LLMs make this**: Debuggers require understanding tool usage; print feels simpler.

**Guard**: Use a debugger. Set breakpoints. Inspect variables. Evaluate expressions.

**Example**:

- Bad: Add 20 print statements to track variable values
- Good: Set breakpoint after suspicious line; step through; inspect variables in REPL

---

### 3. **Not Reproducing Before "Fixing"**

**Mistake**: See error report, make a guess, deploy "fix" without verifying bug first.

**Why LLMs make this**: Seems efficient; avoids setup time.

**Guard**: Reproduce bug locally first. Verify fix resolves it. Test edge cases.

**Example**:

- Bad: Error report says "null pointer"; add null check; deploy
- Good: Reproduce bug → verify null pointer → find root cause → fix → test

---

### 4. **Changing Multiple Things at Once**

**Mistake**: Make 5 changes thinking one will help; can't tell which one fixed it.

**Why LLMs make this**: Feels productive to batch changes.

**Guard**: Change one thing per experiment. Test. If it helps, keep it. If not, revert.

**Example**:

- Bad: Change timeout, add retry, enable logging, modify SQL query, all at once
- Good: Change timeout, test; if it helps, move to next change

---

### 5. **Not Verifying the Fix**

**Mistake**: Make a change; assume it's fixed; don't test thoroughly.

**Why LLMs make this**: Pressure to move on; testing is tedious.

**Guard**: Before closing bug, verify with same steps that triggered it. Test edge cases.

**Example**:

- Bad: Fix division-by-zero error; move on
- Good: Fix division-by-zero; test with zero input; test with negative; test with float

---

### 6. **Fixing Symptoms, Not Root Cause**

**Mistake**: Hide the error instead of fixing the underlying problem.

**Why LLMs make this**: Symptom-fixing is faster; feels complete.

**Guard**: Ask "why did this happen?" Keep asking "why?" until you reach root cause.

**Example**:

- Bad: Error says "null pointer"; add null check; done
- Good: Error says "null pointer"; why is it null? Because initialization was skipped. Why? Input validation missing. Fix validation.

---

## Quality Checklist

Before considering a bug fixed:

- [ ] **Bug reproduced consistently** — Steps are clear, failure is 100% with those steps
- [ ] **Root cause identified** — Not symptom; actual underlying problem
- [ ] **Minimal fix applied** — Only changed what's necessary
- [ ] **Fix verified** — Bug-triggering steps now work correctly
- [ ] **Edge cases tested** — Similar bugs won't reappear with different inputs
- [ ] **Regression test added** — Test prevents bug from reappearing
- [ ] **Code reviewed** — Another engineer confirmed the fix makes sense
- [ ] **No new bugs introduced** — Full test suite passes
- [ ] **Commit message clear** — Explains bug and fix
- [ ] **Monitoring in place** — Alarms/logging if issue occurs again

## Further Reading

- **Andreas Zeller**, _Why Programs Fail: A Guide to Systematic Debugging_ (2nd ed., 2009) — Scientific debugging methodology. Essential reading.
- **Robert C. Martin**, _The Clean Coder_, Chapter 8 (Debugging) — Professionalism and discipline in debugging.
- **John Robbins**, _Debugging Applications_ (2000) — Deep debugging techniques, debugger usage.
- **Steve Maguire**, _Debugging the Development Process_ (1994) — System-level debugging and root cause analysis.
- **Brian Kernighan & Rob Pike**, _The Practice of Programming_ (1999), Chapter 5 — Debugging advice from Unix masters.
