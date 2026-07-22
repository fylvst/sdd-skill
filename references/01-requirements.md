# Phase 1 · Requirements Definition & Clarification

## Goal

Transform a vague initial idea into a clear, unambiguous set of business requirements — answering **what to build** and **why**.

---

## Applicable Scenarios

This phase is triggered when **any** of the following applies:

- The user provides a vague idea or verbal description (e.g., "I want to build feature X").
- The user provides a raw PRD that needs to be structured and made testable.
- The user proposes an iterative improvement to an existing feature (e.g., "Can we change A to B?").
- The user's description is missing user roles, boundary conditions, or acceptance criteria.
- Resuming a previously shelved requirement that needs scope re-confirmation.

> **Not applicable**: If the user has already provided a clear `spec.md` and explicitly says "requirements are confirmed, please produce the design", skip this phase and go directly to Phase 2.

---

## Constraints

The AI must strictly follow these constraints throughout this phase:

| Constraint | Description |
|------------|-------------|
| ✅ **Must produce `spec.md`** | The sole deliverable of this phase is the functional specification; follow the template below |
| ✅ **Must enumerate all acceptance criteria** | Each user story must have at least one testable acceptance criterion (AC) |
| ✅ **Must explicitly state Out of Scope** | List what is not being built to prevent scope creep |
| ❌ **No code of any kind** | Do not output implementation code, pseudocode, or code skeletons in this phase |
| ❌ **No technical design discussion** | Do not discuss architecture choices, tech stack, or database design |
| ❌ **No effort estimation** | Effort estimation belongs to Phase 3; do not perform it here |
| ❌ **No conclusions without clarification** | If requirements are ambiguous, ask clarifying questions before drawing conclusions |
| ❌ **No advancement before alignment** | `spec.md` must be confirmed by the requester before entering Phase 2 |

---

## Inputs

- Raw user request / product brief
- Stakeholder conversations or PRD drafts
- Existing system context (if any)

---

## Activities

1. **Parse the raw request** — identify the core user need behind the stated feature.
2. **Clarify functional boundaries** — what is explicitly in scope, what is out of scope.
3. **Identify user scenarios** — enumerate the key personas and their journeys.
4. **Define acceptance criteria** — concrete, testable conditions that signal "done".
5. **Surface blockers** — list any open questions that must be answered before design can begin.

### Key Questions to Ask

- Who are the target users, and what problem does this solve for them?
- What does success look like from the user's perspective?
- Are there edge cases, error states, or constraints that must be handled?
- What integrations or dependencies are assumed?
- Are there non-functional requirements (performance, security, accessibility)?

---

## Output: `spec.md`

The functional specification document must contain:

| Section | Description |
|---|---|
| **Overview** | One-paragraph summary of the feature and its business value |
| **User Stories** | Written in *"As a [role], I want [goal], so that [benefit]"* format |
| **Acceptance Criteria** | Specific, measurable conditions for each user story |
| **Out of Scope** | Explicit list of excluded functionality |
| **Open Questions** | Unresolved items and their owners |
| **Glossary** | Domain terms with agreed definitions |

📋 Template: [`templates/spec.md`](../templates/spec.md)

---

## Quality Checklist

- [ ] Every user story has at least one acceptance criterion
- [ ] Acceptance criteria are testable (can be verified as pass/fail)
- [ ] No ambiguous terms without a glossary entry
- [ ] All open questions are logged with an owner
- [ ] Scope boundaries are explicitly stated

---

## Transition Criteria to Phase 2

Proceed to **Phase 2 (Plan & Design)** only when:
- All blockers are resolved or have a mitigation plan
- `spec.md` has been reviewed and acknowledged by the requester
- Acceptance criteria are agreed upon
