# ADR-0000: [Decision Title]

> Architecture decisions are **hypotheses**. Fill in "Outcome" after validation — including when the hypothesis was wrong.

| Field | Value |
|-------|-------|
| Status | Proposed / Accepted / Deprecated / Superseded by ADR-XXXX |
| Date | YYYY-MM-DD |
| Deciders | [names or roles] |
| Complexity drivers | [which drivers from `principles.md` made this decision necessary] |

---

## Context

_What is the situation forcing a decision? What constraints exist? What quality attributes are at stake? Keep this factual — no solution bias._

---

## Decision Drivers

- [Driver 1: e.g., "Must support 10k concurrent users without horizontal scaling"]
- [Driver 2: ...]

---

## Options Considered

### Option A: [Name]
- **Pro:** ...
- **Con:** ...

### Option B: [Name]
- **Pro:** ...
- **Con:** ...

### Option C: [Name] _(chosen)_
- **Pro:** ...
- **Con:** ...

---

## Decision

**We choose Option C** because [one sentence linking back to the decision drivers].

Key consequences:
- [Positive consequence]
- [Negative consequence / trade-off accepted]
- [New ADR needed for downstream decision]

---

## Validation Plan

_How will we know this decision was correct? What will we measure, and when?_

- Milestone: [e.g., "After first load test under production-scale data"]
- Signal: [e.g., "P95 latency < 200ms"]

---

## Outcome

_Fill in after validation. Be honest — wrong hypotheses that are documented prevent repeated mistakes._

Date validated: —
Result: [ ] Confirmed  [ ] Partially confirmed  [ ] Invalidated
Notes: —

---

_Update `specs/architecture/overview.md` Decision Index after creating this ADR._
