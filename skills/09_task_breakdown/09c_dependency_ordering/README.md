# 09c 09C Dependency Ordering

## 1. What this sub-SKILL is for

Create a safe implementation order, identify parallelizable groups, blocked tasks, validation prerequisites, and human decisions required before Stage 10 prompt writing.

This is an internal sub-SKILL inside `/skills/09_task_breakdown/`. It is not a standalone public stage contract.

## 2. When to use it

Run it as step 3 in the Stage 9 sequence.

Previous sub-SKILL:

```text
/skills/09_task_breakdown/09b_task_inventory_and_cards/SKILL.md
```

Next sub-SKILL:

```text
/skills/09_task_breakdown/09d_traceability_and_quality_review/SKILL.md
```

## 3. When not to use it

Do not use this sub-SKILL to implement code, write Stage 10 prompts, approve task artifacts, or bypass the parent Stage 9 package.

## 4. Required inputs before running

Read the parent Stage 9 entrypoint first:

```text
/skills/09_task_breakdown/SKILL.md
```

Also read the relevant `/workflow/context` files and the prior Stage 9 outputs required by this sub-SKILL.

## 5. Optional or conditional inputs

Read domain, architecture, API, integration, data, migration, security, privacy, and brownfield artifacts only when they affect this sub-SKILL's responsibility.

## 6. Outputs created when executed

This sub-SKILL creates or updates:

```text
/workflow/09_tasks/09_dependency_order.md
```

These outputs are draft or internal until finalizer consolidation and human approval.

## 7. Human approval requirements

Human approval is required before downstream stages rely on Stage 9 official artifacts. This sub-SKILL may surface decision candidates, assumptions, open questions, and risks, but it must not record agent recommendations as approved decisions.

## 8. How to run in an Agentic Coding tool

1. Start from the parent Stage 9 package.
2. Confirm all prior sub-SKILL outputs required by this step exist.
3. Run this sub-SKILL.
4. Check blocker reports, assumptions, and open questions.
5. Continue to the next sub-SKILL only when safe.

## 9. Relationship to previous and next stages

This sub-SKILL belongs to Stage 9. It prepares or refines artifacts used by the next Stage 9 sub-SKILL. Only the finalizer prepares handoff to Stage 10.

## 10. Status meanings

- `Draft`: Created by the Agent but not approved.
- `Needs Review`: Requires human review before downstream use.
- `Approved`: Explicitly approved by the human developer.

## 11. Common mistakes to avoid

- Treating this sub-SKILL's output as approved final Stage 9 output.
- Skipping prior sub-SKILL outputs.
- Hiding missing required inputs behind assumptions.
- Updating `DECISIONS.md` without explicit human approval.
- Creating project-specific content while maintaining the reusable SKILL package.

## 12. Troubleshooting / blocker cases

Produce a blocker report if required inputs are missing, conflicting, unapproved, superseded, or rejected, or if continuing would create unsafe or unapproved implementation tasks.

## 13. Recommended next step after successful execution

Proceed to:

```text
/skills/09_task_breakdown/09d_traceability_and_quality_review/SKILL.md
```

