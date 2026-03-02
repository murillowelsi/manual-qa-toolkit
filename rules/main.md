# Rules

Conventions that apply to every task without being asked.

---

## ISTQB Principles

Always apply these seven principles when analysing stories or generating test cases:

1. **Testing shows presence of defects** — testing can show defects exist, never prove their absence
2. **Exhaustive testing is impossible** — use risk and priority to focus coverage
3. **Early testing** — flag issues in user stories before development starts
4. **Defect clustering** — a small number of modules contain most defects; focus depth there
5. **Pesticide paradox** — vary test cases; repeated identical tests stop finding new bugs
6. **Testing is context-dependent** — adapt technique to the domain and risk level
7. **Absence-of-errors fallacy** — a passing system that doesn't meet user needs is still a failure

---

## Test Design Techniques

Apply these techniques when generating test cases:

| Technique | When to use |
|-----------|-------------|
| **Equivalence Partitioning (EP)** | Any input with a range of valid/invalid values |
| **Boundary Value Analysis (BVA)** | Numeric ranges, date ranges, string lengths |
| **Decision Table** | Multiple conditions with different outcomes |
| **State Transition** | Workflows, status fields, multi-step processes |
| **Error Guessing** | Based on experience and common failure patterns |
| **Use Case Testing** | End-to-end user journeys |

---

## Risk Framework

Risk Score = **Likelihood (1–5)** × **Impact (1–5)**

| Score | Level | Priority |
|-------|-------|----------|
| 17–25 | Critical | Test first, block release if failing |
| 10–16 | High | Must test before release |
| 5–9 | Medium | Test if time allows |
| 1–4 | Low | Regression / exploratory |

**Likelihood factors**: complexity, recent changes, historical defect rate, unclear requirements
**Impact factors**: financial loss, user-facing, data integrity, regulatory/legal, reputation

---

## User Story Quality Checklist (INVEST)

Every user story must be checked against:

- **I**ndependent — can be developed and tested without depending on another story
- **N**egotiable — details can be discussed, not set in stone
- **V**aluable — delivers value to user or business
- **E**stimable — small and clear enough to estimate
- **S**mall — completable in one sprint
- **T**estable — acceptance criteria can be objectively verified

---

## Acceptance Criteria Quality (SMART)

Each acceptance criterion must be:

- **S**pecific — no vague terms ("fast", "easy", "user-friendly")
- **M**easurable — a pass/fail verdict is possible
- **A**chievable — technically possible
- **R**elevant — relates directly to the story goal
- **T**estable — can be verified by a test case

Flag any criterion containing: *should*, *usually*, *might*, *etc.*, *appropriate*, *reasonable*, *fast*, *easy*.

---

## Test Case Format

Every generated test case must follow this structure:

| Field | Description |
|-------|-------------|
| **ID** | TC-XXX (sequential) |
| **Title** | `should [expected behaviour] when [condition]` |
| **Type** | Positive / Negative / Boundary / Edge Case |
| **Technique** | EP / BVA / Decision Table / State Transition / Error Guessing |
| **Preconditions** | System state before the test |
| **Steps** | Numbered, specific actions |
| **Expected Result** | Exact, verifiable outcome |
| **Risk Level** | Critical / High / Medium / Low |

---

## Output Format

- Analysis reports use structured markdown with emoji severity markers:
  - 🔴 Critical issue (blocks testability or delivery)
  - 🟠 High (significant gap or risk)
  - 🟡 Medium (ambiguity or missing detail)
  - 🟢 Low (suggestion or minor improvement)
- Test case tables are formatted as markdown tables
- Risk matrix is output as a table sorted by Risk Score descending
