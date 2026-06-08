# 04d Domain Events and Bounded Contexts SKILL

## What this sub-skill is for

Define business-significant domain events, workflow implications, bounded contexts, context relationships, and optional context maps.

This sub-skill is an internal part of `/skills/04_domain_modeling/`. It is executable on its own, but downstream stages must not depend on this sub-skill directly.

## When to use it

Use this sub-skill in the required Stage 4 sequence after the previous sub-skill has produced its draft output or after the parent entrypoint confirms that it is the next skill to run.

## When not to use it

Do not use this sub-skill to bypass the Stage 4 finalizer, approve artifacts, create project-specific architecture, database, API, UI, implementation, or test-command decisions, or treat draft outputs as final source of truth.

## Required inputs before running

Always verify the common Stage 4 context inputs listed in the parent `README.md`. This sub-skill additionally requires:

- `/workflow/04_domain/04_ubiquitous_language.md` — Draft ubiquitous language from 04a.
- `/workflow/04_domain/04_domain_model.md` — Draft domain model from 04b/04c.
- `/workflow/04_domain/04_business_rules_invariants.md` — Business rules, invariants, and lifecycle notes from 04c.

## Optional or conditional inputs

Read applicable project intake, brownfield context, risk/privacy screening, Stage 3 traceability, approval log, `USER_DIRECTIVES.md`, review notes, and specialization addenda when they affect this sub-skill's responsibility.

## Outputs created or updated

- `/workflow/04_domain/04_domain_events.md` — Business-significant domain events, causality notes, rejected technical/UI event candidates, and open questions.
- `/workflow/04_domain/04_bounded_contexts.md` — Context strategy, bounded contexts, relationships, single-context rationale, and split candidates.

Conditional outputs:

- `/workflow/04_domain/04_context_map.md` — if Multiple contexts, external contexts, or brownfield context relationships exist.
- `/workflow/04_domain/04_domain_risk_notes.md` — if Security, privacy, compliance, audit, sensitive data, or model risk affects domain rules.
- `/workflow/04_domain/04_domain_model_diagrams.md` — if Diagrams clarify aggregates, contexts, or state transitions.

## Human approval requirements

This sub-skill may surface review items, but Stage 4 is not approval-ready until `04e_domain_modeling_finalizer` runs. Human review is especially needed for:

- Domain events
- Bounded contexts and context relationships
- Single-context rationale, if applicable
- Context split candidates

## How to run this sub-skill in an Agentic Coding tool

1. Read this `SKILL.md`.
2. Read the parent `/skills/04_domain_modeling/SKILL.md` if the public stage contract is unclear.
3. Perform the input preflight and check `USER_DIRECTIVES.md` if it exists.
4. Create or update only the outputs listed above.
5. Record assumptions, open questions, risks, and decision candidates separately.
6. Report handoff notes for the next sub-skill.

## Relationship to previous and next sub-skills

- Previous: `/skills/04_domain_modeling/04c_aggregates_rules_lifecycle/SKILL.md`
- Next: `/skills/04_domain_modeling/04e_domain_modeling_finalizer/SKILL.md`

## Status meanings

- `Draft`: Agent-generated or revised artifact that has not been approved.
- `Needs Review`: Artifact is ready for human review but has unresolved issues or approval needs.
- `Approved`: Human developer explicitly approved the artifact or decision.

## Common mistakes to avoid

- Do not turn domain events into message broker topics.
- Do not equate bounded contexts with microservices or deployment units.
- Do not design API contracts or infrastructure.

## Troubleshooting / blocker cases

Produce a blocker report if required source artifacts are missing, approval status is unclear, inputs conflict, or the sub-skill cannot safely distinguish facts, assumptions, recommendations, and decisions.

## Recommended next step after successful execution

Run `04e_domain_modeling_finalizer` unless this sub-skill is the finalizer. If this is the finalizer, request human review and approval of the official Stage 4 artifacts before Stage 5.
