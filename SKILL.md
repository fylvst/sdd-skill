---
name: sdd-skill
description: >
  Specification-Driven Development (SDD) — a structured six-phase workflow that treats
  the specification as the single source of truth throughout the entire development lifecycle.
  Use this skill whenever you need to take a feature from a vague idea all the way to a
  merged, archived deliverable with full traceability.
version: 1.0.0
---

# SDD · Specification-Driven Development Skill

## Overview

SDD is a structured approach to AI-assisted software development. Rather than jumping straight to code, every phase produces a **living document** that feeds the next phase. This ensures that requirements, design, tasks, code, and validation all stay in sync — with the specification as the **single source of truth**.

```
Phase 1 ──► spec.md
Phase 2 ──► plan.md
Phase 3 ──► tasks.md
Phase 4 ──► proofs.md
Phase 5 ──► validation.md + review.md
Phase 6 ──► archive/<feature>/README.md
```

---

## Document Creation Decision Rules

> **Complete this section's decision flow before entering any phase.**

### 1. Trigger Conditions (When to Activate This Skill)

- Triggered when the user raises a **new feature request, a requirement change, or a technical change request**.
- If the change is trivial — a bug fix, copy update, or config tweak with fewer than 20 lines changed — **do not activate this skill**. Apply the fix and commit directly.

### 2. Document Tier Selection

Choose one of the three modes based on the complexity of the requirement:

| Mode | Applicable Scenario | Documents to Create |
|:-----|:--------------------|:--------------------|
| **Lightweight** | Narrow, low-impact change (e.g., adding a single API endpoint or adjusting one business rule) | `plan.md` only, covering: reason for change, technical approach, impact scope |
| **Standard** | A self-contained user story (e.g., adding a "user points" feature) | `spec.md` + `plan.md`; merge validation records into the end of `plan.md` |
| **Rigorous** | Architecture-level change (e.g., refactoring a core module, replacing a database) | Full document set: `spec.md`, `plan.md`, `tasks.md`, `proofs.md`, `validation.md` |

### 3. Quick Decision Criteria

```
Fewer than 20 lines changed?              → Skip the skill; edit code directly
1–3 files affected, logic is obvious?     → Lightweight mode
New feature module requiring collaboration? → Standard mode
System architecture or critical path?     → Rigorous mode
```

### 4. Document Storage Convention (Isolated Subdirectories)

Each new batch of documents must be stored in a dedicated, timestamped subdirectory. Never mix documents from different batches.

**Directory naming format**: `docs/<YYYY-MM-DD>-<feature-short-name>/`

```
docs/
├── 2026-07-22-user-points/
│   ├── spec.md
│   ├── plan.md
│   └── tasks.md
└── 2026-07-20-refactor-auth/
    ├── spec.md
    └── plan.md
```

**Prohibited**: Do not append to or modify documents in an existing batch directory. Every new requirement — including iterations on an existing feature — must create a new timestamped directory.

**Benefits**:
- Each batch of changes has its own namespace, preventing document overwrites and version confusion.
- The directory structure alone tells you "when" and "what" without reading file metadata.
- Once a feature is complete, the entire directory can be moved to `archive/`, keeping the workspace clean.

### 5. Change Traceability Rule

When creating new documents, if the current change builds on an existing specification, add a reference to the previous version at the top of the document:

```markdown
<!-- Place at the top of the document -->
> Based on: docs/2026-07-15-user-profile/spec.md v1.2
> This change: Add user-points display field
```

Omit this declaration for entirely new features.

---

## Six-Phase Workflow

### Phase 1 — Requirements Definition & Clarification
> **"What are we building, and why?"**

Transforms a vague initial idea into a clear, unambiguous set of business requirements. The AI or developer analyses the raw request, clarifies functional boundaries, identifies user scenarios and edge cases, and agrees on acceptance criteria with the requester.

**Produces**: `spec.md` — functional specification with user stories and acceptance criteria.

📄 Full guide: [`references/01-requirements.md`](references/01-requirements.md)

---

### Phase 2 — Solution Planning & Design
> **"How are we going to build it?"**

Translates the approved spec into a concrete technical blueprint. Activities include analysing the existing codebase, selecting an architecture, designing the data model, defining API contracts, and recording key technical decisions as ADRs.

**Produces**: `plan.md` — architecture overview, data model, API contracts, ADRs, and risk register.

📄 Full guide: [`references/02-planning.md`](references/02-planning.md)

---

### Phase 3 — Task Breakdown
> **"What are the exact steps to build it?"**

Decomposes `plan.md` into an ordered list of atomic, trackable tasks. Tasks are sequenced by dependency, labelled for parallelism, assigned effort sizes, and cross-referenced to acceptance criteria.

**Produces**: `tasks.md` — prioritised task list with file-level change descriptions, dependencies, and traceability links.

📄 Full guide: [`references/03-task-breakdown.md`](references/03-task-breakdown.md)

---

### Phase 4 — Code Implementation
> **"Build it, verify it, commit it."**

Implements each task atomically following the TDD cycle (Red → Green → Refactor). Every completed task is immediately verified and recorded before moving to the next.

**Produces**: Working code + `proofs.md` — a per-task verification log with test evidence.

📄 Full guide: [`references/04-implementation.md`](references/04-implementation.md)

---

### Phase 5 — Validation & Review
> **"Does it match the spec? Is it production-quality?"**

Validates the full implementation against the original acceptance criteria and performs a multi-dimension code review (correctness, security, performance, maintainability, architecture).

**Produces**: `validation.md` (acceptance coverage matrix + E2E results) and `review.md` (code review findings).

📄 Full guide: [`references/05-validation.md`](references/05-validation.md)

---

### Phase 6 — Delivery & Archival
> **"Close the loop. Turn this work into team knowledge."**

Archives all phase documents into a self-contained directory, writes an implementation summary, records key decisions, and propagates learnings to the project knowledge base.

**Produces**: `archive/<feature-slug>/` — a complete, human-readable record of the feature from idea to delivery.

📄 Full guide: [`references/06-delivery.md`](references/06-delivery.md)

---

## Document Traceability Map

| Document | Phase | Purpose |
|----------|-------|---------|
| `spec.md` | 1 | Business requirements & acceptance criteria |
| `plan.md` | 2 | Technical design & key decisions |
| `tasks.md` | 3 | Atomic task list with dependencies |
| `proofs.md` | 4 | Per-task verification evidence |
| `validation.md` | 5 | AC coverage matrix & E2E results |
| `review.md` | 5 | Multi-dimension code review findings |
| `archive/<slug>/README.md` | 6 | Feature summary & knowledge asset |

---

## Phase Transition Rules

Each phase has explicit **entry criteria** (all inputs available and approved) and **exit criteria** (all outputs produced and reviewed). Never skip a phase gate — the spec is the contract.

| From → To | Gate condition |
|-----------|---------------|
| 1 → 2 | `spec.md` reviewed and accepted by requester |
| 2 → 3 | `plan.md` peer-reviewed; high-severity risks mitigated |
| 3 → 4 | `tasks.md` complete, ordered, no dependency cycles |
| 4 → 5 | All tasks done, `proofs.md` complete, CI green |
| 5 → 6 | All ACs pass; High/Medium review findings resolved |
| 6 → ✅ | Archive complete; knowledge base updated |

---

## Quick Reference

```
Need to start a new feature?    → Phase 1: write spec.md
Have a spec, need a design?     → Phase 2: write plan.md
Have a design, need tasks?      → Phase 3: write tasks.md
Have tasks, need to code?       → Phase 4: implement + proofs.md
Code done, need to verify?      → Phase 5: validation.md + review.md
All done, need to archive?      → Phase 6: archive/README.md
```

---

## User Input → Reference Document Routing

When the user says any of the following, load the corresponding reference document before responding.

| User says (keywords / intent) | Load this document |
|-------------------------------|--------------------|
| "I have a requirement", "analyse this requirement", "write spec", "clarify requirements", "user story", "acceptance criteria", "what to build" | [`references/01-requirements.md`](references/01-requirements.md) |
| "write technical design", "write plan", "system design", "architecture design", "data model", "API design", "ADR", "how to implement" | [`references/02-planning.md`](references/02-planning.md) |
| "break down tasks", "write tasks", "task list", "task breakdown", "sprint planning", "task dependencies", "step-by-step plan" | [`references/03-task-breakdown.md`](references/03-task-breakdown.md) |
| "start coding", "implement feature", "write implementation", "TDD", "write tests", "commit code", "proofs" | [`references/04-implementation.md`](references/04-implementation.md) |
| "validate results", "review code", "code review", "run tests", "coverage", "write validation", "security check" | [`references/05-validation.md`](references/05-validation.md) |
| "archive", "deliver", "write summary", "archive feature", "document learnings", "update knowledge base", "close requirement" | [`references/06-delivery.md`](references/06-delivery.md) |

> **Rule**: When in doubt about which phase the user is in, ask one clarifying question:  
> *"Which phase are you currently in? (Requirements / Design / Task Breakdown / Implementation / Validation / Archival)"*  
> Then route to the matching document.
