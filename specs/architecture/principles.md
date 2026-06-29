# Architectural Principles

## Core Premise

Architectural designs are **hypotheses**, not facts. Validate them early with real-world feedback to avoid costly, hard-to-reverse decisions. The purpose of architecture is to enable sound decisions at the right time — minimizing the risk of expensive missteps, not maximizing documentation.

Excessive architecture = waste, delayed feedback, rigidity.
Neglected architecture = chaotic, accidental design, high failure risk.

**The right amount depends entirely on this project's specific needs.**

---

## Building Blocks (from base to apex)

### 1. Communication (foundation)
Team behavior, culture, shared vocabulary, communication norms, and agile mindset. Architecture that lives only in documents fails. Architecture that lives in shared understanding thrives.

- Decisions must be communicated, not just recorded.
- Every ADR has an audience: write for them, not for posterity.
- Architecture thrives on interdisciplinary collaboration — leave the ivory tower.

### 2. Approach
Methodology: when to involve architecture, how decisions are made, how quality is measured, how conformity is checked.

- Architecture work is proportional to complexity drivers.
- Involve architects (or the whole team) at decision points, not just project start.
- Use spikes and prototypes to validate risky assumptions before committing.

### 3. Conceptualization
Technology-agnostic patterns, styles, and recurring problem solutions.

- Prefer established patterns over invented abstractions.
- Document the pattern chosen and why alternatives were rejected (ADR).
- Patterns are candidate solutions, not mandates — match to context.

### 4. Technology (apex)
Specific frameworks, languages, platforms.

- Technology choices follow from approach and conceptualization, not the other way.
- Every technology choice has a cost: learning curve, lock-in, operational overhead.
- Source of truth: the specification (linked in relevant ADRs).

---

## Fit-for-Purpose Rules

| Complexity Driver | Architecture Response |
|---|---|
| High quality / NFR requirements | Add explicit quality specs and acceptance criteria |
| Tight time/budget | Prioritize architectural decisions with highest risk, defer low-risk ones |
| Large or distributed team | Use architecture owner model; increase decision communication |
| New/unfamiliar technology | Require spike before spec; document learnings in ADR |
| External dependencies | Define contracts first; implement against mocks |
| Conflicting goals | Surface conflict explicitly in constitution; resolve before speccing |
| Low complexity, small team | Skip heavyweight phases; go straight to tasks |

---

## Continuous Improvement Loop

```
Architectural Design → Validate Early → Real-World Feedback → Update Design
        ↑___________________________________________________|
```

After every significant delivery, revisit open ADRs and update their "Outcome" section. Designs that proved wrong are more valuable documented than silently fixed.
