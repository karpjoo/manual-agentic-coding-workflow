# 08e Test Strategy Finalizer

## 1. What this sub-SKILL is for

This reusable sub-SKILL is part of the Stage 8 `08_test_strategy_validation` package.

Consolidate Stage 8 artifacts, verify coverage and N/A records, update traceability and context, and prepare the human approval gate.

Core question:

```text
Are the Stage 8 validation artifacts complete, consistent, traceable, and ready for human approval and Stage 9 handoff?
```

## 2. When to use it

Use this sub-SKILL as step 5 in the Stage 8 sequence.

Previous sub-SKILL:

```text
/skills/08_test_strategy_validation/08d_manual_specialized_validation/SKILL.md
```

Next sub-SKILL:

```text
/skills/09_task_breakdown/SKILL.md
```

## 3. When not to use it

Do not use this sub-SKILL to:

- execute the whole Stage 8 package out of order;
- create project-specific requirements, architecture, data design, implementation tasks, or code;
- update `DECISIONS.md` without explicit human approval;
- treat draft outputs as approved artifacts;
- make downstream Stage 9 depend on this internal sub-SKILL directly.

## 4. Required inputs before running

Always check the common workflow context files:

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/APPROVAL_LOG.md
```

Also read the source artifacts listed in this sub-SKILL's `SKILL.md`. If any required input is missing, classify it as blocking or non-blocking before producing output.

## 5. Optional or conditional inputs

Read conditional inputs only when activated by project profile, approved decisions, context, or `USER_DIRECTIVES.md`. Typical conditional inputs include stakeholder/risk screening, domain invariants, API/integration contracts, data design, data security rules, release slices, out-of-scope items, and brownfield context.

## 6. Outputs created when executed

This sub-SKILL creates or updates:

- `/workflow/08_test_strategy/result.md` — Final Stage 8 result and approval gate
- `/workflow/context/TRACEABILITY_MATRIX.md` — Updated validation traceability
- `/workflow/context/context_packet.md` — Stage 9 handoff context


These are project execution artifacts under `/workflow`. They are not created when merely maintaining this reusable SKILL support file.

## 7. Human approval requirements

This sub-SKILL may produce draft artifacts and decision candidates, but it does not approve them. Human approval is normally consolidated at the Stage 8 finalizer.

Record:

- decisions needing approval;
- assumptions needing confirmation;
- open questions affecting validation coverage;
- risks or gaps that may affect Stage 9 task cards.

## 8. How to run this sub-SKILL in an Agentic Coding tool

1. Open this folder's `SKILL.md`.
2. Confirm the previous sub-SKILL output or required stage input exists.
3. Read `/workflow/08_test_strategy/USER_DIRECTIVES.md` if it exists.
4. Perform the input preflight procedure.
5. Create or update only the artifacts assigned to this sub-SKILL.
6. Record assumptions, open questions, validation gaps, and approval needs.
7. Continue to `09_task_breakdown` only after the output is coherent enough for the next sub-SKILL.

## 9. Relationship to parent stage and downstream stage

This sub-SKILL is an internal execution unit. The public Stage 8 contract remains the parent package:

```text
/skills/08_test_strategy_validation/SKILL.md
```

Downstream Stage 9 must depend only on approved official Stage 8 artifacts, not this internal sub-SKILL folder or prompt history.

## 10. How to interpret status values

- `Draft`: Agent-created or revised output awaiting review.
- `Needs Review`: Output is prepared for human review but not approved.
- `Approved`: Human explicitly approved the artifact or decision.

## 11. Common mistakes to avoid

- Running this sub-SKILL out of order without recording why.
- Treating this sub-SKILL's draft as an approved Stage 8 artifact.
- Skipping missing-input classification.
- Using unapproved drafts as source of truth.
- Creating Stage 9 task cards prematurely.
- Claiming tests or commands were executed without evidence.

## 12. Troubleshooting / blocker cases

Produce a blocker report if a required approved input is missing, conflicting, superseded, rejected, or unsafe to assume.

The blocker report should include:

- blocking issue;
- why it matters;
- affected artifacts or stages;
- safe partial work completed;
- human decision needed.

## 13. Recommended next step

After this sub-SKILL completes, run:

```text
/skills/09_task_breakdown/SKILL.md
```
