# Phase 3 · Task Breakdown

## Goal

Decompose the design plan into an ordered, trackable list of atomic tasks — providing a clear execution path for implementation.

---

## Applicable Scenarios

This phase is triggered when **any** of the following applies:

- `plan.md` is complete and has been reviewed; the design is ready to be broken down into executable tasks.
- The user explicitly says "break down tasks", "generate task list", or "create a development plan".
- The team needs to schedule work or divide it for parallel execution.
- You need to identify which tasks can run concurrently to accelerate delivery.
- You are taking over a feature that has a design but no clear execution path.

> **Not applicable**: Do not enter this phase if `plan.md` is not finished, or if the architecture / API contracts are still unstable — design changes will invalidate the task list.

---

## Constraints

In this phase, the AI must strictly adhere to the following constraints:

| Constraint | Description |
|------------|-------------|
| ✅ **Must produce `tasks.md`** | The sole deliverable of this phase is a task list; see the template below for the required format |
| ✅ **Tasks must be atomic** | Each task must be completable within 2–4 hours; any larger task must be broken down further |
| ✅ **Must specify file-level changes** | Each task must explicitly state which files are involved (create / modify) |
| ✅ **Must trace back to acceptance criteria** | Each task must be linked to at least one AC in `spec.md` |
| ✅ **Must identify dependencies** | Inter-task dependencies must be explicitly stated; circular dependencies are not allowed |
| ❌ **No implementation code** | This phase produces only the task list — no code of any kind |
| ❌ **No design decisions in tasks** | Design decisions belong in Phase 2; if a gap is found, return to Phase 2 to fill it |
| ❌ **No missing test tasks** | Every functional task must have a corresponding test-writing task; omitting it is not allowed |

---

## Inputs

- `spec.md` (Phase 1)
- `plan.md` (Phase 2)

---

## Activities

1. **Identify all work units** — enumerate every distinct change required (files to create/modify, migrations, tests, etc.).
2. **Order by dependency** — ensure tasks that depend on others are sequenced correctly.
3. **Flag parallelism** — mark tasks that can be executed concurrently.
4. **Set priority** — distinguish critical-path tasks from nice-to-haves.
5. **Estimate effort** — assign rough size (S / M / L / XL) to aid planning.
6. **Link to spec** — cross-reference each task to the user story or acceptance criterion it satisfies.

### Atomicity Rule

An atomic task must:
- Modify a **bounded, predictable** set of files
- Be completable in a **single focused session** (≤ 2–4 hours)
- Have a **clear done condition** that can be verified independently

If a task is larger, break it down further.

---

## Output: `tasks.md`

The task list document must contain:

| Column | Description |
|---|---|
| **ID** | Unique identifier (e.g. `T-01`) |
| **Title** | Short imperative description |
| **Files affected** | Which files to create or modify |
| **Depends on** | Task IDs this task must wait for |
| **Links to** | Acceptance criteria / ADR this task satisfies |
| **Size** | S / M / L / XL effort estimate |
| **Status** | `pending` / `in_progress` / `done` / `blocked` |

📋 Template: [`templates/tasks.md`](../templates/tasks.md)

---

## Quality Checklist

- [ ] Every acceptance criterion in `spec.md` is covered by at least one task
- [ ] No task depends on an unscheduled or untracked task
- [ ] All tasks include explicit file-level change descriptions
- [ ] Critical-path tasks are clearly separated from parallel or optional work
- [ ] Task sizes are reasonable (nothing larger than XL without sub-tasks)

---

## Transition Criteria to Phase 4

Proceed to **Phase 4 (Implementation)** only when:
- All tasks are listed, ordered, and sized
- Dependencies form a DAG (no cycles)
- At least one engineer has reviewed the list for completeness
