# Paperclip Budget Guidelines

Maps spec-blueprint complexity tiers to Paperclip per-agent monthly budget caps and per-ticket cost estimates.

---

## Budget by Feature Complexity

| Feature complexity | How to identify | Recommended monthly agent budget |
|-------------------|----------------|----------------------------------|
| Low | 1–3 tasks, no external deps, isolated change | $2–5 / agent |
| Medium | 4–10 tasks, one external dep, new component | $10–20 / agent |
| High | 10+ tasks, cross-cutting, new tech, external deps | $30–50 / agent |

---

## Per-Ticket Cost Estimates (model-based)

| Task type | Model | Est. cost per ticket |
|-----------|-------|---------------------|
| Simple (rename, status update, .gitignore) | haiku | < $0.01 |
| Normal (implement CRUD task, update ADR) | sonnet | $0.05–0.20 |
| Complex (architectural planning, /validate on large feature) | opus | $0.50–2.00 |

---

## Budget Hard Stops

Configure these as Paperclip spending limits:

- **spec-reviewer**: $5/month — read-only, haiku, should never exceed this
- **architect**: $20/month — opus, high-value but infrequent
- **implementer (per feature)**: scale with complexity tier above
- **validator**: $10/month — sonnet, runs once per feature

---

## Cost Reduction Levers

1. Tasks already broken down in `tasks.md` → atomic tickets = predictable cost per unit
2. Model Selection in `CLAUDE.md` routes simple tasks to haiku automatically
3. Spec-reviewer gate prevents wasted implementation spend on under-specified features
4. `/explore` (read-only, sonnet) is cheap insurance against expensive wrong-direction builds
