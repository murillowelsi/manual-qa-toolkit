# manual-qa-toolkit

A Claude Code plugin for manual QA testing based on ISTQB principles.

Give it a user story and it analyses it for ambiguities, missing acceptance criteria, and testability issues — then generates structured, risk-prioritised test cases.

---

## Install

```shell
/plugin marketplace add murillowelsi/manual-qa-toolkit
/plugin install manual-qa-toolkit
```

---

## What's included

### Skills

| Skill | Trigger | Description |
|-------|---------|-------------|
| `analyse-story` | `/analyse-story` | Deep analysis of a user story: INVEST check, AC review, missing scenarios |
| `generate-test-cases` | `/generate-test-cases` | Generate test cases using EP, BVA, Decision Tables, State Transition, Error Guessing |
| `assess-risk` | `/assess-risk` | Risk matrix (Likelihood × Impact) and prioritised execution order |

### Commands

| Command | Description |
|---------|-------------|
| `/qa-review` | Full pipeline: analyse story + generate test cases + risk prioritisation in one shot |
| `/rewrite-story` | Rewrite a story in Given/When/Then format with fixed ACs and missing error paths |

### Agents

| Agent | Description |
|-------|-------------|
| `story-analyser` | Proactively flags the top issues when a user story is shared in the conversation |

---

## How it works

### Quick triage
Paste a user story into the chat. The `story-analyser` agent immediately flags the most critical issues.

### Deep analysis
Run `/analyse-story` for a full ISTQB-based review:
- Checks the story against the **INVEST** criteria
- Reviews each acceptance criterion for ambiguity, incompleteness, and testability
- Identifies missing scenarios: error paths, boundaries, permissions, security

### Test case generation
Run `/generate-test-cases` to get structured test cases using:
- **Equivalence Partitioning** — valid/invalid input classes
- **Boundary Value Analysis** — edge values for ranges
- **Decision Tables** — complex condition combinations
- **State Transition** — workflows and status flows
- **Error Guessing** — common failure patterns from experience

### Risk prioritisation
Run `/assess-risk` to score each test case by **Likelihood × Impact** and get a recommended execution order by phase (Critical → High → Medium → Low).

### Full pipeline
Run `/qa-review` to get everything in one consolidated document.

### Story rewrite
Run `/rewrite-story` to get a clean, testable version of the story in Given/When/Then format with all gaps addressed.

---

## Example workflow

```
1. Paste user story in chat
   → story-analyser agent flags top issues immediately

2. /analyse-story
   → Full INVEST check + AC review + missing scenario report

3. /rewrite-story
   → Clean Given/When/Then rewrite with fixed ACs

4. /generate-test-cases
   → Full test case table with coverage matrix

5. /assess-risk
   → Risk matrix + recommended execution order
```

Or shortcut everything:

```
/qa-review → full document in one command
```

---

## ISTQB Principles Applied

1. Testing shows presence of defects — not absence
2. Exhaustive testing is impossible — use risk to focus
3. Early testing — flag story issues before dev starts
4. Defect clustering — deeper coverage on high-risk areas
5. Pesticide paradox — vary test cases across techniques
6. Context-dependent — adapt to domain and risk level
7. Absence-of-errors fallacy — a passing system that misses the goal still fails
