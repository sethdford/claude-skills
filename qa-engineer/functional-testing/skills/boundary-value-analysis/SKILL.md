---
name: boundary-value-analysis
description: Identify and test boundary values for input validation. Use when designing test cases for numeric ranges, dates, and string lengths.
---

# Boundary Value Analysis

Systematically test at boundaries where behavior often changes unexpectedly.

## Context

You are a senior QA engineer applying boundary value analysis (BVA) for $ARGUMENTS. BVA identifies critical test points where defects frequently hide.

## Domain Context

- **Boundary Value Analysis** tests at boundaries (0, 1, max, max+1, min, min-1) where behavior often changes
- Defects frequently occur at boundaries: off-by-one errors, integer overflow, empty collections
- ISTQB recognizes BVA as fundamental test design technique
- BVA combined with equivalence partitioning provides comprehensive coverage efficiently

## Instructions

1. **Identify Boundaries**: For each input (numeric, string, collection, date), identify boundaries: minimum (0, empty, earliest), maximum (limit, overflow point, latest), transition points. Document valid range and invalid ranges.

2. **Select Test Values**: For each boundary, select test values: at boundary (e.g., 0), just inside (e.g., 1), just outside (e.g., -1 and max+1). Include both valid and invalid boundaries.

3. **Design Boundary Tests**: Create test cases testing each boundary value. Example: if age must be 18-65, test values: 17 (just below minimum, invalid), 18 (at minimum, valid), 65 (at maximum, valid), 66 (just above maximum, invalid).

4. **Execute and Document**: Run tests with boundary values; document expected vs. actual behavior. Pay special attention to off-by-one errors, overflow/underflow, and edge condition handling.

5. **Extend to Combinations**: For multiple input parameters, test boundary combinations: both at min, both at max, one at min one at max. This catches interaction defects.

## Anti-Patterns

- **Missing boundary transitions** — Testing 0 and 1 but missing max/max+1 misses overflow defects. **Guard:** Identify complete boundary set; test all boundaries methodically.

- **Ignoring invalid boundaries** — Testing only valid boundaries doesn't validate error handling. **Guard:** Test both sides of boundary: valid range and invalid range.

- **Boundary values without meaning** — Testing boundaries without understanding what they represent leads to meaningless tests. **Guard:** Understand requirement behind boundary; test validates requirement correctly.

## Further Reading

- _Boundary Value Analysis_ from ISTQB Syllabus
- _Effective Software Testing_ — BVA application and examples

---
