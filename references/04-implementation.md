# Phase 4 · Code Implementation

## Goal

Incrementally implement each task from `tasks.md`, validating each piece before proceeding — producing working code anchored to the specification.

---

## Applicable Scenarios

This phase is triggered when **any** of the following applies:

- `tasks.md` is complete and has been reviewed; coding can begin.
- The user explicitly says "start coding", "implement the feature", or "begin development".
- You are working on a specific task (e.g., "implement T-03 now").
- Tasks are to be completed and validated incrementally using TDD.
- A CI failure needs to be fixed and maps to a specific task.

> **Not applicable**: Do not start coding if `tasks.md` is not finished, or if prerequisite tasks for the current task are not yet complete.

---

## Constraints

In this phase, the AI must strictly adhere to the following constraints:

| Constraint | Description |
|------------|-------------|
| ✅ **Must follow task order** | Implement strictly in the dependency order defined in `tasks.md`; no skipping ahead |
| ✅ **Must write tests first** | Follow TDD: write the failing test first, then write the implementation, then refactor |
| ✅ **Must update `proofs.md` after each task** | Record verification evidence (test output or screenshot) immediately; do not backfill later |
| ✅ **Each task must be a separate commit** | One commit per task; commit message format must follow the convention |
| ✅ **Code must follow project standards** | Style, lint rules, and naming conventions must conform to the existing codebase |
| ❌ **No implementing features outside `spec.md`** | Do not add undocumented features or parameters "while you are at it" |
| ❌ **No committing with failing tests** | All local tests must pass before committing; never commit with a red build |
| ❌ **No mixing multiple tasks in one commit** | Multiple tasks must not be merged into a single commit; this harms traceability |
| ❌ **No modifying `spec.md` or `plan.md`** | If an issue with requirements or design is found during implementation, stop and notify; do not modify upstream documents unilaterally |

---

## Inputs

- `spec.md` (Phase 1)
- `plan.md` (Phase 2)
- `tasks.md` (Phase 3)

---

## Implementation Principles

### Specification-Driven
Every line of code should be traceable to a task, which traces to an acceptance criterion, which traces to a user story. Do not implement features not covered by the spec.

### Test-Driven Development (TDD)
Follow the Red → Green → Refactor cycle:
1. **Red** — write a failing test that captures the acceptance criterion.
2. **Green** — write the minimum code to make the test pass.
3. **Refactor** — clean up without changing behaviour; tests must remain green.

### Atomic Commits
One commit per completed task. Commit message format:
```
<type>(T-XX): <short imperative description>

- AC-XX: <which criterion this satisfies>
- Files: <list of changed files>
```

---

## Activities

For each task in `tasks.md` (in dependency order):

1. **Read the task** — understand the files to change and the acceptance criteria to satisfy.
2. **Write the test first** — unit, integration, or e2e depending on the layer.
3. **Implement the minimum code** — make the test pass.
4. **Run all tests** — confirm no regressions.
5. **Refactor if needed** — improve clarity, remove duplication.
6. **Update `tasks.md`** — mark task as `done`.
7. **Record proof** — append a verification entry to `proofs.md`.
8. **Commit** — atomic commit with a meaningful message.

---

## Output: `proofs.md`

A living verification log updated after each task:

| Column | Description |
|---|---|
| **Task** | Task ID completed |
| **AC covered** | Acceptance criteria validated |
| **Verification method** | Unit test / integration test / manual check |
| **Evidence** | Test output snippet or screenshot reference |
| **Timestamp** | When verified |

📋 Template: [`templates/proofs.md`](../templates/proofs.md)

---

## Quality Checklist

- [ ] Every committed task has a corresponding entry in `proofs.md`
- [ ] All tests pass locally before committing
- [ ] No committed code is commented-out dead code
- [ ] Code follows the project's style guide and lint rules
- [ ] No hardcoded credentials, secrets, or environment-specific values

---

## Transition Criteria to Phase 5

Proceed to **Phase 5 (Validation & Review)** only when:
- All tasks in `tasks.md` are marked `done`
- `proofs.md` has an entry for every task
- CI pipeline passes (all tests green, no lint errors)
