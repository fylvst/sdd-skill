# Phase 5 · Validation & Review

## Goal

Verify the implementation against the original specification end-to-end, and evaluate code quality across multiple dimensions — ensuring the deliverable is correct, secure, and maintainable.

---

## Applicable Scenarios

This phase is triggered when **any** of the following applies:

- All tasks are marked `done`, `proofs.md` is complete, CI is fully green, and the branch is ready to merge.
- The user explicitly says "validate results", "review code", or "perform code review".
- A PR has been submitted and a systematic quality assessment of the entire feature branch is needed.
- A coverage matrix is required to confirm every acceptance criterion has test coverage.
- A targeted check is needed for security compliance, performance, or architectural consistency.

> **Not applicable**: Do not enter this phase if any tasks are still incomplete or CI has a failing build. Return to Phase 4 to resolve those issues first.

---

## Constraints

In this phase, the AI must strictly adhere to the following constraints:

| Constraint | Description |
|------------|-------------|
| ✅ **Must produce `validation.md`** | A validation matrix covering all ACs, with each item marked Pass / Fail / Missing |
| ✅ **Must produce `review.md`** | A multi-dimension code review report with a severity level for every finding |
| ✅ **`spec.md` is the sole acceptance baseline** | "The code looks fine" does not substitute for verifying each AC individually |
| ✅ **Must cover the security dimension** | At minimum, check input validation, access control, and sensitive data exposure |
| ❌ **No approving with unresolved High-severity findings** | Critical issues must be fixed; recording them without blocking the merge is not allowed |
| ❌ **No modifying business code** | This phase is review and reporting only; issues found must be returned to Phase 4 for fixes — do not edit code in this phase |
| ❌ **No omitting any AC from `spec.md`** | `validation.md` must cover every acceptance criterion; selective validation is not allowed |
| ❌ **No subjective language in review findings** | Every finding must reference a specific file and line number; vague conclusions such as "code quality is poor" are not allowed |

---

## Inputs

- `spec.md` — acceptance criteria to validate against
- `plan.md` — architectural decisions to verify were honoured
- `proofs.md` — task-level evidence from Phase 4
- Full codebase diff of the feature branch

---

## Validation Activities

### 1. Acceptance Criteria Coverage Matrix

For every acceptance criterion in `spec.md`, confirm:
- Which test(s) exercise it
- Whether that test is passing
- Coverage percentage for the affected code paths

### 2. End-to-End Scenario Testing

Walk through each user story from `spec.md` in a realistic environment:
- Happy path
- Error / edge case paths
- Boundary conditions

### 3. Regression Check

Confirm no pre-existing tests were broken.

---

## Code Review Activities

Perform a multi-dimension review of all changed files:

| Dimension | Questions to ask |
|---|---|
| **Correctness** | Does the code do what the spec says? Are edge cases handled? |
| **Security** | Input validation, SQL injection, XSS, auth checks, secrets exposure? |
| **Performance** | N+1 queries, missing indexes, unbounded loops, memory leaks? |
| **Readability** | Clear naming, appropriate comments, consistent style? |
| **Maintainability** | DRY, single responsibility, test coverage? |
| **Architecture** | Does the implementation honour the decisions in `plan.md`? |

---

## Outputs

📋 Template: [`templates/validation.md`](../templates/validation.md)

📋 Template: [`templates/review.md`](../templates/review.md)

---

## Quality Checklist

- [ ] Every acceptance criterion has a status (Pass / Fail / Missing)
- [ ] All `Fail` or `Missing` items have a linked follow-up task or known exception
- [ ] All `High` severity review findings are resolved before merge
- [ ] Coverage meets or exceeds the project threshold
- [ ] No new lint warnings introduced

---

## Transition Criteria to Phase 6

Proceed to **Phase 6 (Delivery & Archival)** only when:
- All acceptance criteria are `Pass`
- All `High` and `Medium` severity findings are resolved or explicitly accepted with owner sign-off
- Final CI run is fully green
