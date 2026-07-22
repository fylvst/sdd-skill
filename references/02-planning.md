# Phase 2 · Solution Planning & Design

## Goal

Translate business requirements into a concrete technical blueprint — answering **how to build it**.

---

## Applicable Scenarios

This phase is triggered when **any** of the following applies:

- `spec.md` is complete and confirmed by the requester, and requirements need to be translated into a technical blueprint
- The user explicitly says "write technical design", "system design", or "define the architecture"
- Multiple technical paths need to be evaluated and a technology choice must be made
- A new requirement affects the existing architecture and the scope of change needs to be assessed
- API contracts or data models need to be aligned with other teams

> **Not applicable**: If `spec.md` is not yet complete or requirements are still ambiguous, Phase 1 must be finished first. Do not enter this phase.

---

## Constraints

The AI must strictly follow these constraints in this phase:

| Constraint | Description |
|------|------|
| ✅ **Must produce `plan.md`** | The sole deliverable of this phase is the technical design document; see the template below |
| ✅ **Must use `spec.md` as the baseline** | All design decisions must be traceable to acceptance criteria in `spec.md` |
| ✅ **Must record ADRs** | Every significant technical decision must document its context, options considered, and rationale |
| ✅ **Must list risks explicitly** | Technical risks and their mitigations must be written into `plan.md` |
| ❌ **No implementation code** | This phase produces design documents only — no functional or test code |
| ❌ **Do not define APIs before the data model is complete** | The data model is the foundation for APIs; it must be finalised first |
| ❌ **Do not introduce requirements not covered by `spec.md`** | If a gap is found, return to Phase 1 to add it rather than expanding the design unilaterally |
| ❌ **Do not proceed before review** | `plan.md` must be reviewed by at least one other engineer before entering Phase 3 |

---

## Inputs

- `spec.md` (from Phase 1, fully signed off)
- Existing codebase analysis
- Relevant team conventions and ADRs (Architecture Decision Records)

---

## Activities

1. **Analyse the existing codebase** — understand current architecture, patterns, and constraints.
2. **Architecture selection** — choose architectural style, layers, and component boundaries.
3. **Data model design** — define entities, relationships, and storage strategy.
4. **API / interface contract** — specify public interfaces, endpoints, events, or messages.
5. **Record key technical decisions** — capture the rationale for major choices as ADRs.
6. **Identify risks and mitigations** — surface technical risks early.

### Design Principles

- Prefer the simplest solution that satisfies the acceptance criteria.
- Make implicit decisions explicit by writing them down.
- Favour reversible decisions over irreversible ones.
- Identify the narrowest stable interface between components.

---

## Output: `plan.md`

The technical design document must contain:

| Section | Description |
|---|---|
| **Architecture Overview** | Diagram or description of major components and their relationships |
| **Data Model** | Entity definitions, field types, constraints, relationships |
| **API / Interface Contracts** | Endpoint signatures, request/response schemas, events |
| **Key Technical Decisions** | ADR-style records: context → options → decision → rationale |
| **Risks & Mitigations** | Identified technical risks with planned responses |
| **Dependencies** | External services, libraries, or team deliverables this work depends on |

📋 Template: [`templates/plan.md`](../templates/plan.md)

---

## Quality Checklist

- [ ] Architecture diagram or description covers all major components
- [ ] Data model covers all entities referenced in `spec.md`
- [ ] Every public interface has a defined contract (schema / signature)
- [ ] At least one ADR recorded for each significant technical choice
- [ ] All acceptance criteria from `spec.md` are traceable to design decisions

---

## Transition Criteria to Phase 3

Proceed to **Phase 3 (Task Breakdown)** only when:
- `plan.md` has been peer-reviewed by at least one other engineer
- All high-severity risks have mitigations
- API contracts are stable enough to begin parallel development
