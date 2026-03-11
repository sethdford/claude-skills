# TDD Cycle Example: Shopping Cart Feature

## Feature/Story

Shopping cart system for e-commerce application. Users should be able to add items to cart, view total price, and apply discount codes.

## Requirement

The shopping cart must accurately calculate the total price including tax, applying discount codes when provided.

---

## Cycle 1: Calculate Total Without Items

### Red: Write Test

```python
def test_shopping_cart_returns_zero_for_empty_cart():
    cart = ShoppingCart()
    assert cart.total_price() == 0.00
```

**Expected failure**: `AttributeError: 'ShoppingCart' object has no attribute 'total_price'`

### Green: Implement

```python
class ShoppingCart:
    def total_price(self) -> float:
        return 0.00
```

### Verify

- **Test passes**: Yes
- **Suite passes**: Yes (first test)
- **Regressions**: None

### Refactor

No refactoring needed for this simple implementation.

## Summary

The shopping cart now has a `total_price()` method that returns 0.00 for an empty cart. This is the foundation for more complex logic.

## Next Test

Test that adding a single item updates the total price: `test_shopping_cart_returns_item_price_with_one_item`.

---

## Cycle 2: Add Single Item

### Red: Write Test

```python
def test_shopping_cart_returns_item_price_with_one_item():
    cart = ShoppingCart()
    cart.add_item("Widget", 10.00)
    assert cart.total_price() == 10.00
```

**Expected failure**: `TypeError: add_item() missing 2 required positional arguments: 'name' and 'price'`

### Green: Implement

```python
class ShoppingCart:
    def __init__(self):
        self.items = []

    def add_item(self, name: str, price: float) -> None:
        self.items.append({"name": name, "price": price})

    def total_price(self) -> float:
        if not self.items:
            return 0.00
        return sum(item["price"] for item in self.items)
```

### Verify

- **Test passes**: Yes
- **Suite passes**: Yes (both tests pass)
- **Regressions**: None

### Refactor

No refactoring needed; implementation is clear and minimal.

## Summary

The shopping cart now supports adding items and calculating total price. Price is calculated as the sum of all item prices.

## Next Test

Test that multiple items are summed correctly: `test_shopping_cart_sums_multiple_items`.

---

## Cycle 3: Add Multiple Items

### Red: Write Test

```python
def test_shopping_cart_sums_multiple_items():
    cart = ShoppingCart()
    cart.add_item("Widget", 10.00)
    cart.add_item("Gadget", 5.50)
    cart.add_item("Doohickey", 2.25)
    assert cart.total_price() == 17.75
```

**Expected failure**: Assertion would fail if implementation didn't sum correctly. Current implementation should pass.

### Green: Implement

(No new implementation needed; current code already handles multiple items via the sum.)

### Verify

- **Test passes**: Yes
- **Suite passes**: Yes (all three tests pass)
- **Regressions**: None

### Refactor

No refactoring needed; the implementation is already general enough.

## Summary

Multiple items are now correctly summed. The cart can handle any number of items and calculate the total.

## Next Test

Test that discount codes reduce the total: `test_shopping_cart_applies_discount_code`.

---

## Cycle 4: Apply Discount Code

### Red: Write Test

```python
def test_shopping_cart_applies_discount_code():
    cart = ShoppingCart()
    cart.add_item("Widget", 100.00)
    cart.apply_discount_code("SAVE10")  # 10% off
    assert cart.total_price() == 90.00
```

**Expected failure**: `AttributeError: 'ShoppingCart' object has no attribute 'apply_discount_code'`

### Green: Implement

```python
class ShoppingCart:
    # Discount code to percentage mapping (naive: hardcoded)
    DISCOUNT_CODES = {
        "SAVE10": 0.10,  # 10% off
        "SAVE20": 0.20,  # 20% off
    }

    def __init__(self):
        self.items = []
        self.discount_code = None

    def add_item(self, name: str, price: float) -> None:
        self.items.append({"name": name, "price": price})

    def apply_discount_code(self, code: str) -> None:
        if code in self.DISCOUNT_CODES:
            self.discount_code = code

    def total_price(self) -> float:
        if not self.items:
            return 0.00
        subtotal = sum(item["price"] for item in self.items)
        if self.discount_code and self.discount_code in self.DISCOUNT_CODES:
            discount_percent = self.DISCOUNT_CODES[self.discount_code]
            return subtotal * (1 - discount_percent)
        return subtotal
```

### Verify

- **Test passes**: Yes
- **Suite passes**: Yes (all four tests pass)
- **Regressions**: None. Existing tests still pass because discount_code is None by default.

### Refactor

The discount calculation logic is separate from the sum, which is clear. No refactoring needed yet.

## Summary

The shopping cart now supports discount codes. When a valid code is applied, the total price is reduced by the specified percentage.

## Next Test

Test that invalid discount codes are ignored: `test_shopping_cart_ignores_invalid_discount_code`.

---

## Cycle 5: Ignore Invalid Discount Code

### Red: Write Test

```python
def test_shopping_cart_ignores_invalid_discount_code():
    cart = ShoppingCart()
    cart.add_item("Widget", 100.00)
    cart.apply_discount_code("INVALID_CODE_THAT_DOES_NOT_EXIST")
    assert cart.total_price() == 100.00  # No discount applied
```

**Expected failure**: Would fail if invalid codes were not handled. Current implementation should pass.

### Green: Implement

(No new implementation needed; current code already checks if code is in DISCOUNT_CODES.)

### Verify

- **Test passes**: Yes
- **Suite passes**: Yes (all five tests pass)
- **Regressions**: None

### Refactor

No refactoring needed; the implementation is already defensive.

## Summary

Invalid discount codes are now safely ignored, and the full price is returned.

---

## Cycle 6: Add Tax Calculation

### Red: Write Test

```python
def test_shopping_cart_applies_tax_to_subtotal():
    cart = ShoppingCart()
    cart.add_item("Widget", 100.00)
    # Assume 10% tax rate
    total = cart.total_price()  # $100 + $10 tax = $110
    assert total == 110.00
```

**Expected failure**: Test would fail because current implementation doesn't include tax.

### Green: Implement

```python
class ShoppingCart:
    TAX_RATE = 0.10  # 10% tax
    DISCOUNT_CODES = {
        "SAVE10": 0.10,
        "SAVE20": 0.20,
    }

    def __init__(self):
        self.items = []
        self.discount_code = None

    def add_item(self, name: str, price: float) -> None:
        self.items.append({"name": name, "price": price})

    def apply_discount_code(self, code: str) -> None:
        if code in self.DISCOUNT_CODES:
            self.discount_code = code

    def total_price(self) -> float:
        if not self.items:
            return 0.00
        subtotal = sum(item["price"] for item in self.items)
        if self.discount_code and self.discount_code in self.DISCOUNT_CODES:
            discount_percent = self.DISCOUNT_CODES[self.discount_code]
            subtotal = subtotal * (1 - discount_percent)
        tax = subtotal * self.TAX_RATE
        return round(subtotal + tax, 2)
```

### Verify

- **Test passes**: Yes
- **Suite passes**: Yes (all tests pass)
- **Regressions**: None. Existing tests now include tax, which is expected behavior.

### Refactor

The `total_price()` method is getting complex. Extract a helper for tax calculation:

```python
class ShoppingCart:
    TAX_RATE = 0.10
    DISCOUNT_CODES = {
        "SAVE10": 0.10,
        "SAVE20": 0.20,
    }

    def __init__(self):
        self.items = []
        self.discount_code = None

    def add_item(self, name: str, price: float) -> None:
        self.items.append({"name": name, "price": price})

    def apply_discount_code(self, code: str) -> None:
        if code in self.DISCOUNT_CODES:
            self.discount_code = code

    def _calculate_subtotal(self) -> float:
        """Calculate subtotal before tax, after discounts."""
        if not self.items:
            return 0.00
        subtotal = sum(item["price"] for item in self.items)
        if self.discount_code and self.discount_code in self.DISCOUNT_CODES:
            discount_percent = self.DISCOUNT_CODES[self.discount_code]
            subtotal = subtotal * (1 - discount_percent)
        return subtotal

    def _apply_tax(self, subtotal: float) -> float:
        """Apply tax to subtotal."""
        return subtotal * (1 + self.TAX_RATE)

    def total_price(self) -> float:
        """Calculate total price including tax and discounts."""
        subtotal = self._calculate_subtotal()
        return round(self._apply_tax(subtotal), 2)
```

### Verify

- **Test passes**: Yes
- **Suite passes**: Yes (all tests still pass after refactoring)
- **Regressions**: None

## Summary

Tax is now applied to the subtotal after discounts. The code is clearer with helpers for subtotal and tax calculations. The shopping cart now fully supports:

- Adding items
- Calculating subtotal
- Applying discount codes
- Applying tax
- Returning a rounded total price

---

## Final Output

The shopping cart implementation is now complete for the core feature. The TDD approach allowed the feature to grow incrementally, with each test driving one behavior at a time.

**Key learnings from this example**:

1. Each test should verify one behavior
2. Implementations start simple and evolve as tests require
3. Refactoring happens after several cycles when patterns emerge
4. Tests serve as a safety net for refactoring
5. Final implementation is clean and well-structured because the design emerged from tests
