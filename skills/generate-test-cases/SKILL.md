---
name: generate-test-cases
description: Generate structured, ISTQB-compliant test cases from a user story. Applies Equivalence Partitioning, Boundary Value Analysis, Decision Tables, State Transition, and Error Guessing. Use after analyse-story or when the user provides a story to test.
---

# Generate Test Cases

Generate comprehensive, prioritised test cases from a user story using ISTQB test design techniques.

## Input

If not already provided, ask for:
- The user story and acceptance criteria
- Any analysis output from `analyse-story` (if available)
- Domain context (e.g. e-commerce, banking, healthcare) for error guessing

---

## Step 1 — Identify Test Conditions

For each acceptance criterion, derive **test conditions** — the aspects that need to be covered:

```
AC: "User can filter products by category"
Test conditions:
  - Valid category selected → results filtered correctly
  - Invalid/non-existent category → appropriate error or empty state
  - No category selected → all products shown
  - Multiple categories selected (if supported)
  - Category with 0 results
```

List all test conditions before generating test cases.

---

## Step 2 — Apply Test Design Techniques

### Equivalence Partitioning (EP)

Divide inputs into valid and invalid partitions. One test per partition is sufficient.

```
Input: age field (valid: 18–99)
Valid partition: any value 18–99 (test with e.g. 30)
Invalid partition 1: < 18 (test with e.g. 15)
Invalid partition 2: > 99 (test with e.g. 100)
Invalid partition 3: non-numeric (test with e.g. "abc")
```

### Boundary Value Analysis (BVA)

Test at the boundary and just inside/outside it.

```
Range: 1–100
Test values: 0, 1, 2, 99, 100, 101
```

### Decision Table

Use when multiple conditions determine an outcome.

```
| Condition A | Condition B | Expected Outcome |
|-------------|-------------|-----------------|
| True        | True        | Result X        |
| True        | False       | Result Y        |
| False       | True        | Result Z        |
| False       | False       | Result W        |
```

### State Transition

Use for workflows, status fields, and multi-step processes.

```
States: Draft → Submitted → Approved / Rejected
Test each valid transition and each invalid one (e.g. Draft → Approved directly)
```

### Error Guessing

Based on experience and common failure patterns:
- Empty inputs on required fields
- Special characters in text fields (`<script>`, `'`, `--`)
- Very long strings exceeding DB limits
- Concurrent actions by multiple users
- Session expiry mid-action
- Slow network / timeout scenarios

---

## Step 3 — Write Test Cases

For each test condition, write a complete test case:

| ID | Title | Type | Technique | Preconditions | Steps | Expected Result | Risk |
|----|-------|------|-----------|---------------|-------|-----------------|------|
| TC-001 | should filter products when valid category selected | Positive | EP | User logged in, products exist in category | 1. Go to product list<br>2. Select category "Electronics"<br>3. Click Apply | Only products in "Electronics" are displayed | High |
| TC-002 | should show empty state when category has no products | Edge Case | EP | User logged in, category exists with 0 products | 1. Go to product list<br>2. Select empty category<br>3. Click Apply | Empty state message displayed, no error | Medium |

**Test naming**: always `should [expected behaviour] when [condition]`

**Test types to always include**:
- ✅ At least one positive (happy path) test per AC
- ❌ At least one negative test per AC
- 🔲 Boundary tests for any numeric/date input
- ⚠️ At least one error guessing test per story

---

## Step 4 — Coverage Summary

After generating tests, produce a coverage matrix:

| AC | Happy Path | Unhappy Path | Boundary | Edge Case | Error Guessing |
|----|-----------|--------------|----------|-----------|----------------|
| AC1 | ✅ TC-001 | ✅ TC-003 | ✅ TC-005 | ✅ TC-002 | ✅ TC-006 |
| AC2 | ✅ TC-007 | ❌ Missing | — | — | ✅ TC-008 |

Flag any gap in the coverage matrix.

---

## After Generating

Ask the user:
1. Do you want me to **prioritise these test cases by risk**? → use `assess-risk`
2. Do you want to **export this as a test plan**? → `/qa-review`
