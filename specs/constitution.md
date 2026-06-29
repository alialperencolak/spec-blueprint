# Project Constitution

> The constitution defines non-negotiable principles. All architectural decisions, feature specs, and implementation choices must be consistent with these. If a decision conflicts with the constitution, raise it explicitly rather than silently violating it.

---

## Purpose

_What is this project for? Who does it serve?_

<!-- Example: "Enable small teams to ship reliable software without sacrificing speed." -->

---

## Non-Negotiable Principles

_List 3–7 principles that are load-bearing for this project. These are constraints, not goals._

1. **[Principle name]** — [One sentence explaining the constraint and why it is inviolable.]
2. **[Principle name]** — ...
3. **[Principle name]** — ...

---

## Quality Gates

Every shipped feature must satisfy:

- [ ] Has a passing spec (`specs/features/<name>/spec.md` acceptance criteria all green)
- [ ] Has no regressions in existing spec acceptance criteria
- [ ] Architectural decisions are documented as ADRs if they affect more than one subsystem
- [ ] Contracts (APIs, events, schemas) are versioned and backward-compatible unless explicitly breaking

---

## Out of Scope

_What will this project explicitly NOT do? Captures YAGNI decisions made early._

- ...

---

## Stakeholders & Architecture Role

| Role | Person/Team | Responsibilities |
|------|------------|-----------------|
| Architecture owner | — | Overall architectural vision, cross-cutting decisions |
| Architecture champions | — | Domain-specific topics (e.g., security, data) |
| Development team | — | Feature-level architectural decisions within principles |

---

_Last updated: [date] by [who]_
