---
name: analyse-story
description: Analyse a user story using ISTQB principles. Finds ambiguities, missing acceptance criteria, inconsistencies, and testability issues. Use when a user story is provided for QA review.
---

# Analyse Story

Perform a deep QA analysis of a user story before test design begins.

## Input

Ask the user to provide:
- The user story text
- Any related acceptance criteria
- Context: feature area, domain, dependent stories (if available)

---

## Step 1 — Parse the Story

Extract and restate:
- **Role**: Who is the user?
- **Goal**: What do they want to do?
- **Benefit**: Why do they want it?
- **Acceptance Criteria**: List each one numbered

If the story is missing Role, Goal, or Benefit, flag immediately as 🔴.

---

## Step 2 — INVEST Check

Evaluate each criterion:

| Criterion   | Pass / Fail | Notes                                       |
|-------------|-------------|---------------------------------------------|
| Independent | ✅ / ❌     | Does it depend on another unfinished story? |
| Negotiable  | ✅ / ❌     | Are details overly prescriptive?            |
| Valuable    | ✅ / ❌     | Is the business/user value clear?           |
| Estimable   | ✅ / ❌     | Is scope clear enough to estimate?          |
| Small       | ✅ / ❌     | Can it be completed in one sprint?          |
| Testable    | ✅ / ❌     | Can each AC be verified objectively?        |

---

## Step 3 — Acceptance Criteria Analysis

For each AC, check:

**Ambiguity** — vague terms with no measurable definition:
- Flag: *should*, *usually*, *might*, *fast*, *easy*, *user-friendly*, *appropriate*, *reasonable*, *etc.*
- Example: "The system should respond quickly" → 🔴 What is "quickly"? Define in ms/s.

**Incompleteness** — what is not covered:
- What happens on error? (empty input, invalid format, network failure)
- What happens at boundaries? (max/min values, empty state, single item)
- What are the permissions? (authenticated vs guest, role differences)
- What are the negative paths? (what should NOT happen)

**Contradiction** — ACs that conflict with each other or with the story goal.

**Testability** — can a tester write a pass/fail test for this?

---

## Step 4 — Missing Scenarios

Identify scenarios the story does not address:

- **Happy path** — is the main success flow fully described?
- **Unhappy paths** — validation errors, system errors, unauthorised access
- **Boundary conditions** — min/max values, empty states, single records
- **Concurrency** — what if two users act simultaneously?
- **Performance** — are there SLAs or load expectations?
- **Security** — can a user access another user's data? Are inputs sanitised?
- **Accessibility** — any specific requirements?
- **Mobile/responsive** — if applicable

---

## Step 5 — Risk Identification

For each gap or ambiguity found, assign a risk level:
- 🔴 **Critical** — blocks test design or delivery; requires clarification before dev starts
- 🟠 **High** — significant gap; likely to cause defects if unaddressed
- 🟡 **Medium** — ambiguous detail; may cause inconsistent implementation
- 🟢 **Low** — minor suggestion; improves clarity but not blocking

---

## Output Format

```markdown
## Story Analysis Report

### Story Summary
- **As a**: [role]
- **I want**: [goal]
- **So that**: [benefit]

### INVEST Check
| Criterion   | Status  | Notes |
|-------------|---------|-------|
| Independent | ✅ / ❌ |       |
...

### Acceptance Criteria Review

**AC1**: [text]
- Status: ✅ Clear / ⚠️ Ambiguous / ❌ Untestable
- Issues: [list]

...

### Missing Scenarios
🔴 [Critical gap]
🟠 [High gap]
🟡 [Medium gap]
🟢 [Low suggestion]

### Recommended Next Steps
1. Clarify: [specific question for PO/BA]
2. Add AC: [suggested criterion]
3. Split story: [if too large]
```

---

## After Analysis

Ask the user:
1. Do you want me to **rewrite the story** with the issues fixed? → `/rewrite-story`
2. Do you want me to **generate test cases** from this story? → `/generate-test-cases`
3. Do you want a **full QA review** (analysis + test cases + risk prioritisation)? → `/qa-review`
