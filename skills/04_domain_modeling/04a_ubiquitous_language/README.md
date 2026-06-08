# 04a Ubiquitous Language SKILL

## What this sub-skill is for

Extract, normalize, and stabilize domain vocabulary from approved requirements and related inputs.

This sub-skill is an internal part of `/skills/04_domain_modeling/`. It is executable on its own, but downstream stages must not depend on this sub-skill directly.

## When to use it

Use this sub-skill in the required Stage 4 sequence after the previous sub-skill has produced its draft output or after the parent entrypoint confirms that it is the next skill to run.

## When not to use it

Do not use this sub-skill to bypass the Stage 4 finalizer, approve artifacts, create project-specific architecture, database, API, UI, implementation, or test-command decisions, or treat draft outputs as final source of truth.

## Required inputs before running

Always verify the common Stage 4 context inputs listed in the parent `README.md`. This sub-skill additionally requires:

- No additional sub-skill-specific required input beyond common Stage 4 inputs.

## Optional or conditional inputs

Read applicable project intake, brownfield context, risk/privacy screening, Stage 3 traceability, approval log, `USER_DIRECTIVES.md`, review notes, and specialization addenda when they affect this sub-skill's responsibility.

## Outputs created or updated

- `/workflow/04_domain/04_ubiquitous_language.md` — Preferred domain terms, synonyms, deprecated terms, ambiguity, and handoff notes.

Conditional outputs:

- None for this sub-skill.

## Human approval requirements

This sub-skill may surface review items, but Stage 4 is not approval-ready until `04e_domain_modeling_finalizer` runs. Human review is especially needed for:

- Preferred ubiquitous language terms
- Deprecated/rejected terms
- Ambiguous terminology requiring domain expert resolution

## How to run this sub-skill in an Agentic Coding tool

1. Read this `SKILL.md`.
2. Read the parent `/skills/04_domain_modeling/SKILL.md` if the public stage contract is unclear.
3. Perform the input preflight and check `USER_DIRECTIVES.md` if it exists.
4. Create or update only the outputs listed above.
5. Record assumptions, open questions, risks, and decision candidates separately.
6. Report handoff notes for the next sub-skill.

## Relationship to previous and next sub-skills

- Previous: `Parent entrypoint / previous Stage 3 official artifacts`
- Next: `/skills/04_domain_modeling/04b_domain_concepts_entities_values/SKILL.md`

## Status meanings

- `Draft`: Agent-generated or revised artifact that has not been approved.
- `Needs Review`: Artifact is ready for human review but has unresolved issues or approval needs.
- `Approved`: Human developer explicitly approved the artifact or decision.

## Common mistakes to avoid

- Do not classify every term as an entity.
- Do not design database tables, APIs, UI, or architecture.
- Do not silently resolve terminology conflicts.

## Troubleshooting / blocker cases

Produce a blocker report if required source artifacts are missing, approval status is unclear, inputs conflict, or the sub-skill cannot safely distinguish facts, assumptions, recommendations, and decisions.

## Recommended next step after successful execution

Run `04b_domain_concepts_entities_values` unless this sub-skill is the finalizer. If this is the finalizer, request human review and approval of the official Stage 4 artifacts before Stage 5.
