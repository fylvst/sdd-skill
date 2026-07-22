# Phase 6 · Delivery & Archival

## Goal

Close the development loop by archiving all artefacts into a self-contained knowledge asset — turning a completed feature into reusable team knowledge.

---

## Applicable Scenarios

This phase is triggered when **any** of the following applies:

- `validation.md` and `review.md` have fully passed, and the code has been merged to the main branch.
- The user explicitly says "archive", "deliver", "write summary", or "close the requirement".
- The feature has been deployed to production and the team needs to document learnings and conduct a retrospective.
- The team needs a complete feature delivery record for future maintenance or auditing.
- Key decisions and lessons from this development cycle should be distilled into team knowledge base entries.

> **Not applicable**: Do not enter this phase if validation has not passed or the code has not yet been merged. Complete all blocking items in Phase 5 first.

---

## Constraints

In this phase, the AI must strictly adhere to the following constraints:

| Constraint | Description |
|------------|-------------|
| ✅ **Must produce `archive/<slug>/README.md`** | Must include an implementation summary, key decisions, known trade-offs, and lessons learned |
| ✅ **Must archive all six phase documents** | `spec.md`, `plan.md`, `tasks.md`, `proofs.md`, `validation.md`, and `review.md` must all be included |
| ✅ **Must update the project knowledge base** | Any ADR log, onboarding documentation, or runbook entries relevant to this cycle must be updated accordingly |
| ✅ **Must record trade-offs and outstanding issues** | Known technical debt or unfinished optimisations must be documented and tracked in the issue tracker |
| ❌ **No glossing over or concealing problems** | Archive documents must faithfully record every problem encountered and every compromise made; only writing positive content is not allowed |
| ❌ **No archiving before code is merged** | Archiving is only permitted once the code is in the main branch; premature or false archiving is not allowed |
| ❌ **No omitting Lessons Learned** | Every archive must include at least one "improve next time" lesson; leaving it blank is not allowed |

---

## Inputs

- All phase documents: `spec.md`, `plan.md`, `tasks.md`, `proofs.md`, `validation.md`, `review.md`
- Merged code in the main branch
- CI/CD deployment confirmation

---

## Activities

1. **Confirm delivery** — verify the feature is deployed (or released) and monitoring is healthy.
2. **Assemble the archive** — collect all phase documents into a canonical directory.
3. **Write the decision summary** — distil the most important architectural and product decisions.
4. **Write the implementation summary** — one-page narrative of what was built and how.
5. **Update the project knowledge base** — propagate learnings to shared docs, ADR log, or wiki.
6. **Retrospective notes** — capture what went well and what to improve next cycle.

---

## Archive Directory Structure

```
archive/<feature-slug>/
├── README.md          ← implementation summary + key decisions
├── spec.md            ← requirements (from Phase 1)
├── plan.md            ← technical design (from Phase 2)
├── tasks.md           ← task list with final statuses (from Phase 3)
├── proofs.md          ← implementation evidence (from Phase 4)
├── validation.md      ← acceptance validation report (from Phase 5)
└── review.md          ← code review report (from Phase 5)
```

---

## Output: `archive/<feature-slug>/README.md`

The archive summary document:

📋 Template: [`templates/archive-readme.md`](../templates/archive-readme.md)

---

## Knowledge Base Updates

After archiving, propagate relevant learnings:

| Target | What to update |
|--------|----------------|
| **ADR log** | Append any new architectural decisions made during this cycle |
| **Onboarding docs** | Update if new patterns or tools were introduced |
| **Runbook / ops docs** | Add operational notes if the feature requires monitoring or maintenance |
| **Shared component library** | Extract and document any reusable components built |

---

## Quality Checklist

- [ ] All six phase documents are present in the archive directory
- [ ] `README.md` is written and human-readable without needing the other documents
- [ ] Key decisions are recorded with rationale (not just "what" but "why")
- [ ] Known trade-offs and follow-up work are logged in the issue tracker
- [ ] Project knowledge base / wiki has been updated

---

## Cycle Complete

Once this phase is done, the SDD cycle for this feature is **closed**.  
The archive serves as the single source of truth for future maintainers, auditors, or anyone re-opening this work.
