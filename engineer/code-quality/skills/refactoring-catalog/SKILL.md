---
name: refactoring-catalog
description: Proven refactoring patterns (Extract Method, Replace Temp, Introduce Parameter Object) to improve code structure safely. Use when improving existing code while keeping behavior unchanged.
context: fork
agent: general-purpose
allowed-tools: Read, Grep, Glob, Write, Edit, Bash
---

# Refactoring Catalog

Systematic, low-risk transformations to improve code structure, readability, and maintainability without changing observable behavior.

## Context

You are guiding code improvement through safe refactoring. Your role is to:

- Identify refactoring opportunities (duplication, poor names, long methods, complex conditionals)
- Apply proven transformations from Martin Fowler's catalog
- Use tests as a safety net to ensure behavior is preserved
- Keep changes small and focused (one refactoring per commit)
- Document the rationale for each refactoring

Refactoring is the art of cleaning house without breaking anything. Each refactoring is tiny, testable, and immediately verifiable.

## Domain Context

Based on Martin Fowler's _Refactoring_ and Michael Feathers' _Working Effectively with Legacy Code_:

- **Red-Green-Refactor Cycle**: Refactor only when tests are green. Tests are the safety net.
- **Small Steps**: Each refactoring should be a 5-minute task. If it takes longer, break it down.
- **Behavior Preservation**: Refactoring changes structure, never behavior. Observable inputs/outputs remain identical.
- **Baby Steps**: Commit frequently. Each commit should be revertible and self-contained.
- **Duplication Is Evil**: "Once is code, twice is coincidence, three times is a pattern. Extract."
- **Names Matter**: Spend time on clear, intention-revealing names. Better names = lower cognitive load.

## When to Use This Skill

- Code has duplication across multiple locations
- Method names don't clearly express intent
- A function is doing multiple things (low cohesion)
- Conditional logic is deeply nested or complex
- Parameters are loosely related and could be grouped
- Coupling between classes is high; methods belong elsewhere
- After implementing a feature, code needs improvement (Refactor phase of TDD)
- Preparing code for a large change (improve structure first)

## Prerequisites

Before refactoring, ensure:

- **Tests Are Green**: All tests pass. Refactoring is a destructive operation if tests fail.
- **Test Coverage**: Code should have good test coverage (70%+) in the area being refactored
- **Small Scope**: Refactoring only in the module/class at hand; don't refactor the whole system at once
- **Clear Criteria**: Know what "better" looks like (clarity, cohesion, reduced duplication)
- **Time**: Refactoring takes focus; don't multitask or rush

## Instructions (Detailed)

### 1. **Identify the Refactoring Opportunity**

Read the code and ask:

- Are there similar code blocks in multiple places? → Extract Method / Consolidate Duplicate Code
- Does a variable have a vague name? → Rename Variable
- Is the function doing multiple things? → Extract Method / Extract Class
- Are parameters unrelated? → Introduce Parameter Object
- Is there a boolean flag parameter? → Replace Flag Argument with Methods
- Is there a complex conditional chain? → Replace Conditional with Polymorphism
- Does a method belong to a different class? → Move Method

**Example identifying refactoring opportunities**:

```python
# Poor: Vague names, duplicated logic, multiple responsibilities
def process_order(order):
    subtotal = 0
    for item in order.items:
        subtotal += item.price * item.qty
    subtotal *= 0.95  # 5% discount (magic number!)
    if order.is_vip:
        subtotal *= 0.9  # another 10% for VIP
    tax = subtotal * 0.08
    total = subtotal + tax
    print(f"Total: {total}")
    if total > 100:
        order.flag_for_priority_shipping()
    return total
```

Refactoring opportunities:

- Extract `calculate_subtotal()` (duplicated calculation logic across similar methods)
- Extract `apply_discount()` (separate discount logic)
- Extract `apply_tax()` (separate tax logic)
- Replace magic numbers with named constants
- Extract `is_priority_order()` check (readability)

### 2. **Write/Verify Tests Cover the Code**

Before refactoring, ensure tests cover the behavior you'll change:

```python
def test_process_order_calculates_correct_total():
    order = Order(items=[
        Item("Widget", 50, 2),   # 2x Widget @ $50 = $100
        Item("Gadget", 25, 1)    # 1x Gadget @ $25 = $25
    ], is_vip=False)
    # Subtotal: $125 → -5% discount = $118.75 → +8% tax = $128.25
    assert process_order(order) == 128.25

def test_process_order_vip_discount():
    order = Order(items=[
        Item("Widget", 100, 1)
    ], is_vip=True)
    # Subtotal: $100 → -5% = $95 → -10% = $85.50 → +8% tax = $92.34
    assert process_order(order) == 92.34

def test_process_order_flags_priority_for_large_orders():
    order = Order(items=[
        Item("Widget", 60, 2)  # $120
    ], is_vip=False)
    process_order(order)
    assert order.priority_shipping_flagged is True
```

Run these tests. They pass with the current (messy) code. Now refactor with confidence.

### 3. **Apply First Refactoring: Extract Method**

**Goal**: Move duplicated or complex logic into a helper method.

**Before**:

```python
def process_order(order):
    subtotal = 0
    for item in order.items:
        subtotal += item.price * item.qty
    subtotal *= 0.95
    if order.is_vip:
        subtotal *= 0.9
    tax = subtotal * 0.08
    total = subtotal + tax
    # ... more logic
```

**After**:

```python
def process_order(order):
    subtotal = self._calculate_subtotal(order)
    subtotal = self._apply_discount(subtotal, order.is_vip)
    total = self._apply_tax(subtotal)
    # ... more logic

def _calculate_subtotal(self, order):
    """Sum of all item prices (unit price * quantity)."""
    subtotal = 0
    for item in order.items:
        subtotal += item.price * item.qty
    return subtotal

def _apply_discount(self, subtotal, is_vip):
    """Apply standard 5% discount, plus 10% for VIP."""
    subtotal *= 0.95
    if is_vip:
        subtotal *= 0.9
    return subtotal

def _apply_tax(self, subtotal):
    """Apply 8% sales tax."""
    return subtotal * 1.08
```

**Run tests**: All tests should pass. Behavior is identical.

**Commit**: `refactor: extract discount and tax logic into helper methods`

### 4. **Apply Next Refactoring: Replace Magic Numbers**

**Goal**: Replace hardcoded numbers with named constants.

**Before**:

```python
def _apply_discount(self, subtotal, is_vip):
    subtotal *= 0.95     # What is 0.95?
    if is_vip:
        subtotal *= 0.9  # What is 0.9?
    return subtotal

def _apply_tax(self, subtotal):
    return subtotal * 1.08  # What is 1.08?
```

**After**:

```python
STANDARD_DISCOUNT_RATE = 0.05  # 5% discount
VIP_DISCOUNT_RATE = 0.10       # Additional 10% for VIP
SALES_TAX_RATE = 0.08          # 8% sales tax

def _apply_discount(self, subtotal, is_vip):
    subtotal *= (1 - self.STANDARD_DISCOUNT_RATE)
    if is_vip:
        subtotal *= (1 - self.VIP_DISCOUNT_RATE)
    return subtotal

def _apply_tax(self, subtotal):
    return subtotal * (1 + self.SALES_TAX_RATE)
```

**Run tests**: All tests should pass.

**Commit**: `refactor: replace magic numbers with named constants`

### 5. **Apply Next Refactoring: Replace Conditional with Method**

**Goal**: Replace boolean flag parameters with separate, well-named methods.

**Before**:

```python
def process_order(order, include_tax=True):  # Flag parameter; confusing
    subtotal = self._calculate_subtotal(order)
    subtotal = self._apply_discount(subtotal, order.is_vip)
    if include_tax:
        total = self._apply_tax(subtotal)
    else:
        total = subtotal
    return total
```

**After**:

```python
def process_order(order):
    """Calculate order total including all discounts and taxes."""
    subtotal = self._calculate_subtotal(order)
    subtotal = self._apply_discount(subtotal, order.is_vip)
    total = self._apply_tax(subtotal)
    return total

def calculate_order_subtotal(order):
    """Calculate order total without taxes (for internal use)."""
    subtotal = self._calculate_subtotal(order)
    subtotal = self._apply_discount(subtotal, order.is_vip)
    return subtotal
```

Now callers choose the appropriate method name, making intent clear.

**Run tests**: All tests should pass.

**Commit**: `refactor: replace include_tax flag parameter with distinct methods`

### 6. **Apply Refactoring: Move Method**

**Goal**: Move a method to the class that uses it most, improving cohesion.

**Before**:

```python
class Order:
    def process(self):
        # ...
        total = order_processor._apply_tax(subtotal)

class OrderProcessor:
    def _apply_tax(self, subtotal):
        return subtotal * (1 + TAX_RATE)
```

**After** (Tax logic belongs to Order, not OrderProcessor):

```python
class Order:
    def apply_tax(self, subtotal):
        """Apply sales tax to subtotal."""
        return subtotal * (1 + TAX_RATE)

    def process(self):
        # ...
        total = self.apply_tax(subtotal)

class OrderProcessor:
    # _apply_tax removed; moved to Order
```

**Run tests**: All tests should pass.

**Commit**: `refactor: move tax calculation to Order class`

### 7. **Look for Remaining Duplication**

Scan for copy-paste code:

**Before**:

```python
def format_price_usd(price):
    return f"${price:.2f}"

def format_price_eur(price):
    return f"€{price:.2f}"

def format_price_gbp(price):
    return f"£{price:.2f}"
```

**After**:

```python
def format_price(price, currency_symbol="$"):
    return f"{currency_symbol}{price:.2f}"
```

Or use a Currency object for better abstraction.

**Run tests**: All tests should pass.

**Commit**: `refactor: consolidate currency formatting`

### 8. **Verify Final State**

After a series of refactorings:

- Run full test suite
- Code is clearer and more maintainable
- No behavior changed (tests still pass)
- Each refactoring is reversible (can see in git history)

## Output Format

When using this skill, deliver:

1. **Refactoring Identified**: What refactoring technique is being applied? Why?
2. **Before Code**: Original code showing the problem
3. **After Code**: Refactored code showing the improvement
4. **Verification**: Tests still pass; behavior unchanged
5. **Commit Message**: Conventional commit format

Example output:

```
## Refactoring: Extract Method

**Identified Problem**:
Discount calculation is duplicated across `process_order()` and `calculate_order_subtotal()`.

**Before**:
[code showing duplication]

**After**:
[code with helper method]

**Tests**: All pass. Behavior unchanged.

**Commit Message**:
refactor: extract discount calculation into helper method
```

## Worked Example: Simplifying a Payment Processor

**Starting code** (smelly):

```python
class PaymentProcessor:
    def process_payment(self, amount, customer_type, apply_fee=True):
        # Validate amount
        if amount <= 0:
            raise ValueError("Invalid amount")

        # Calculate fee based on customer type
        fee = 0
        if customer_type == "premium":
            fee = amount * 0.01
        elif customer_type == "standard":
            fee = amount * 0.025
        else:
            fee = amount * 0.05

        # Apply fee
        if apply_fee:
            total = amount + fee
        else:
            total = amount

        # Process
        print(f"Processing ${total} for {customer_type} customer")
        return total
```

**Refactoring 1: Extract Method for validation**

```python
def _validate_amount(self, amount):
    if amount <= 0:
        raise ValueError("Invalid amount")

def process_payment(self, amount, customer_type, apply_fee=True):
    self._validate_amount(amount)
    fee = self._calculate_fee(amount, customer_type)
    if apply_fee:
        total = amount + fee
    else:
        total = amount
    print(f"Processing ${total} for {customer_type} customer")
    return total
```

**Refactoring 2: Extract fee calculation**

```python
def _calculate_fee(self, amount, customer_type):
    """Calculate processing fee based on customer type."""
    fee_rates = {
        "premium": 0.01,
        "standard": 0.025,
        "standard": 0.05,  # default
    }
    rate = fee_rates.get(customer_type, 0.05)
    return amount * rate
```

**Refactoring 3: Replace flag parameter with methods**

```python
def process_payment(self, amount, customer_type):
    """Process payment including fees."""
    self._validate_amount(amount)
    return self._calculate_total_with_fee(amount, customer_type)

def process_payment_without_fee(self, amount, customer_type):
    """Process payment without fees."""
    self._validate_amount(amount)
    return amount

def _calculate_total_with_fee(self, amount, customer_type):
    fee = self._calculate_fee(amount, customer_type)
    total = amount + fee
    print(f"Processing ${total} for {customer_type} customer")
    return total
```

**Final refactored state**:

```python
class PaymentProcessor:
    FEE_RATES = {
        "premium": 0.01,
        "standard": 0.025,
        "basic": 0.05,
    }

    def process_payment(self, amount, customer_type):
        """Process payment with fees."""
        self._validate_amount(amount)
        fee = self._calculate_fee(amount, customer_type)
        total = amount + fee
        self._log_transaction(total, customer_type)
        return total

    def process_payment_without_fee(self, amount, customer_type):
        """Process payment without fees (e.g., internal transfers)."""
        self._validate_amount(amount)
        return amount

    def _validate_amount(self, amount):
        if amount <= 0:
            raise ValueError("Invalid amount")

    def _calculate_fee(self, amount, customer_type):
        rate = self.FEE_RATES.get(customer_type, 0.05)
        return amount * rate

    def _log_transaction(self, amount, customer_type):
        print(f"Processing ${amount} for {customer_type} customer")
```

Each refactoring:

- Has a clear purpose
- Is tested (behavior unchanged)
- Is committed separately
- Makes code easier to understand

## Decision Framework

When refactoring, use these decisions:

- **If duplicated >2 times**: Extract to shared method or function
- **If method >15 lines**: Too long; extract helpers
- **If variable name unclear**: Rename it immediately (takes 30 seconds)
- **If conditional logic nested >2 levels deep**: Extract method or use guard clause
- **If parameter list >4 arguments**: Group related ones into Parameter Object
- **If class >300 lines**: Too large; consider splitting into multiple classes
- **If tests take >5 seconds to run**: Refactor towards faster unit tests (fewer integration tests)
- **If refactoring takes >15 minutes**: You're doing too much; break into smaller steps

## Anti-Patterns (Expanded)

### 1. **Refactoring Without Tests**

**Mistake**: Change code structure without test coverage; hope nothing breaks.

**Why LLMs make this**: Confidence in code changes without safety net.

**Guard**: Before refactoring any code, ensure tests pass and cover the area being refactored (70%+ coverage).

**Example**:

- Bad: Refactor `calculate_discount()` without tests; verify manually
- Good: Ensure tests pass for `calculate_discount()` before refactoring

---

### 2. **Mixing Refactoring and Feature Work**

**Mistake**: In one commit/PR, both refactor code AND add a new feature.

**Why LLMs make this**: Feels efficient to clean up while implementing.

**Guard**: Separate refactoring commits from feature commits. Reviewers can't distinguish intent if mixed.

**Example**:

- Bad: PR: "Extract tax logic AND add new tax rate" (1 commit)
- Good: PR 1: "Extract tax logic" (refactoring), PR 2: "Add new tax rate" (feature)

---

### 3. **Extracting Methods Too Early (YAGNI)**

**Mistake**: Create helper methods for code that isn't duplicated.

**Why LLMs make this**: Speculative abstractions feel like good engineering.

**Guard**: Wait until you see duplication 2-3 times before extracting. One method alone is just splitting for no reason.

**Example**:

- Bad: Extract `_format_debug_message()` when used once
- Good: Use the code inline; extract when used in 2+ places

---

### 4. **Large, Unfocused Refactorings**

**Mistake**: Refactor many things in one commit (rename variables, extract methods, move classes).

**Why LLMs make this**: Completing the whole improvement feels productive.

**Guard**: One refactoring per commit. If it takes >15 minutes, break into smaller commits.

**Example**:

- Bad: "refactor: extract methods, rename variables, reorganize" (30 files)
- Good: "refactor: extract calculate_tax method" (2 files)

---

### 5. **Not Running Tests Between Refactorings**

**Mistake**: Make multiple refactorings, then run tests once.

**Why LLMs make this**: Batching feels efficient.

**Guard**: Run tests after each refactoring (every 5-15 minutes). Rapid feedback reveals problems immediately.

**Example**:

- Bad: Rename 5 variables, extract 3 methods, run tests once
- Good: Rename 1 variable, run tests; extract 1 method, run tests; repeat

---

### 6. **Ignoring Performance Impact**

**Mistake**: Refactor for clarity; accidentally introduce performance regression.

**Why LLMs make this**: Focus on readability; miss runtime implications.

**Guard**: Profile before and after refactoring. "Replace Temp with Query" introduces function calls; measure impact.

**Example**:

- Bad: Extract `calculate_total()` that's called in a loop 10,000x
- Good: Profile first; if in hot path, keep inline or cache result

---

## Quality Checklist

Before considering a refactoring complete, verify:

- [ ] **All tests pass** — Run full suite; no failures or errors
- [ ] **No behavior change** — Inputs and outputs are identical to before
- [ ] **Code is clearer** — Names are better, structure is simpler, duplication is reduced
- [ ] **One concern per commit** — Refactoring only; no feature changes mixed in
- [ ] **Refactoring is small** — Can be reviewed quickly; <50 lines changed ideally
- [ ] **Not over-engineered** — Didn't extract prematurely; waited for duplication to emerge
- [ ] **Performance verified** — Profiled hot paths; no regressions
- [ ] **Commit message is clear** — Explains what refactoring and why
- [ ] **Revertible** — Can be undone if needed; has test safety net
- [ ] **Readable by others** — Another engineer can understand the refactoring intent

## Further Reading

- **Martin Fowler**, _Refactoring: Improving the Design of Existing Code_ (2nd ed., 2018) — The canonical reference. Read Chapters 6-9 for specific refactorings with detailed before/after.
- **Michael Feathers**, _Working Effectively with Legacy Code_ (2004) — How to refactor code without tests (Characterization Tests).
- **Kent Beck**, _Implementation Patterns_ (2007) — Philosophy and patterns for clean code structure.
- **Sandro Mancuso**, _The Software Craftsman_ (2014) — Professionalism and disciplined refactoring as a daily practice.
- **Robert C. Martin**, _Clean Code_ (2008) — Naming, function design, error handling; all driven by refactoring.
- **Joshua Kerievsky**, _Refactoring to Patterns_ (2004) — How refactoring evolves code toward design patterns naturally.
