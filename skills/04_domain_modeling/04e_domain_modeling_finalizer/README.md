# 04e Domain Modeling Finalizer SKILL

## What this sub-skill is for

Consolidate Stage 4 official artifacts, update traceability and context handoff, record N/A decisions, and prepare the human approval gate.

This sub-skill is an internal part of `/skills/04_domain_modeling/`. It is executable on its own, but downstream stages must not depend on this sub-skill directly.

## When to use it

Use this sub-skill in the required Stage 4 sequence after the previous sub-skill has produced its draft output or after the parent entrypoint confirms that it is the next skill to run.

## When not to use it

Do not use this sub-skill to bypass the Stage 4 finalizer, approve artifacts, create project-specific architecture, database, API, UI, implementation, or test-command decisions, or treat draft outputs as final source of truth.

## Required inputs before running

Always verify the common Stage 4 context inputs listed in the parent `README.md`. This sub-skill additionally requires:

- `/workflow/04_domain/04_ubiquitous_language.md` — Ubiquitous language from 04a.
- `/workflow/04_domain/04_domain_model.md` — Domain model from 04b/04c.
- `/workflow/04_domain/04_business_rules_invariants.md` — Rules, invariants, aggregates, and lifecycle outputs from 04c.
- `/workflow/04_domain/04_domain_events.md` — Domain events from 04d.
- `/workflow/04_domain/04_bounded_contexts.md` — Bounded contexts from 04d.

## Optional or conditional inputs

Read applicable project intake, brownfield context, risk/privacy screening, Stage 3 traceability, approval log, `USER_DIRECTIVES.md`, review notes, and specialization addenda when they affect this sub-skill's responsibility.

## Outputs created or updated

- `/workflow/04_domain/04_domain_traceability_matrix.md` — Requirement-to-domain and domain-to-future-stage traceability.
- `/workflow/04_domain/result.md` — Stage 4 result summary, decisions, assumptions, open questions, N/A records, consistency review, and approval gate.
- `/workflow/context/context_packet.md` — Minimal operational handoff for Stage 5.

Conditional outputs:

- None for this sub-skill.

## Human approval requirements

This sub-skill may surface review items, but Stage 4 is not approval-ready until `04e_domain_modeling_finalizer` runs. Human review is especially needed for:

- All Stage 4 official artifacts ready for review
- Traceability gaps and risk-sensitive domain notes
- Stage 5 handoff context
- Assumptions and open questions that may affect architecture

## How to run this sub-skill in an Agentic Coding tool

1. Read this `SKILL.md`.
2. Read the parent `/skills/04_domain_modeling/SKILL.md` if the public stage contract is unclear.
3. Perform the input preflight and check `USER_DIRECTIVES.md` if it exists.
4. Create or update only the outputs listed above.
5. Record assumptions, open questions, risks, and decision candidates separately.
6. Report handoff notes for the next sub-skill.

## Relationship to previous and next sub-skills

- Previous: `/skills/04_domain_modeling/04d_events_bounded_contexts/SKILL.md`
- Next: `05_architecture_contracts`

## Status meanings

- `Draft`: Agent-generated or revised artifact that has not been approved.
- `Needs Review`: Artifact is ready for human review but has unresolved issues or approval needs.
- `Approved`: Human developer explicitly approved the artifact or decision.

## Common mistakes to avoid

- Do not approve artifacts on behalf of the human developer.
- Do not update DECISIONS.md without explicit human approval.
- Do not create new architecture, database, API, UI, implementation, or test-command decisions.

## Troubleshooting / blocker cases

Produce a blocker report if required source artifacts are missing, approval status is unclear, inputs conflict, or the sub-skill cannot safely distinguish facts, assumptions, recommendations, and decisions.

## Recommended next step after successful execution

Run `05_architecture_contracts` unless this sub-skill is the finalizer. If this is the finalizer, request human review and approval of the official Stage 4 artifacts before Stage 5.
