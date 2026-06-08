---
name: 12e_review_release_finalizer
description: Consolidate Stage 12 review artifacts, classify blockers/warnings/suggestions, update traceability, prepare context for Stage 13, and present the final human approval gate.
stage: 12 Review / Security / Release / Handoff
parent_skill: /skills/12_review_release_handoff/SKILL.md
subskill_id: 12e
subskill_order: 5
previous_subskill: /skills/12_review_release_handoff/12d_operations_documentation_handoff/SKILL.md
next_subskill: /skills/13_retrospective/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/12_review_release_handoff/result.md
requires_human_approval: true
external_visibility: internal
---

# 12e Review / Release Finalizer

## 1. Purpose

This finalizer consolidates all Stage 12 sub-SKILL outputs into official Stage 12 handoff artifacts.

It prepares the final human approval gate for:

- release readiness;
- deployment readiness;
- security/privacy risk acceptance;
- accepted limitations;
- migration/rollback readiness;
- operations ownership;
- documentation handoff.

It also prepares `context_packet.md` for Stage 13 Workflow Retrospective & Skill Improvement.

This finalizer does not approve release or deployment. It only prepares the decision package.

## 2. Core Question

```text
What is the final Stage 12 release/handoff decision package, what evidence supports it, what blockers or warnings remain, and what must be handed to Stage 13 for workflow retrospective?
```

## 3. Required Inputs

### Always Read

```text
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/APPROVAL_LOG.md

/workflow/12_review_release_handoff/12_code_review.md
/workflow/12_review_release_handoff/12_security_privacy_review.md
/workflow/12_review_release_handoff/12_release_readiness.md
/workflow/12_review_release_handoff/12_documentation_handoff.md
```

### Read If Applicable

```text
/workflow/12_review_release_handoff/12_deployment_plan.md
- if deployment is in scope.

/workflow/12_review_release_handoff/12_operations_runbook.md
- if operation, support, monitoring, or maintenance is in scope.

/workflow/12_review_release_handoff/12_release_notes.md
- if versioned or handoff release notes exist.

/workflow/12_review_release_handoff/12_migration_readiness.md
- if migration is in scope.

/workflow/12_review_release_handoff/12_incident_rollback_plan.md
- if separate rollback/recovery planning exists.

/workflow/12_review_release_handoff/12_compliance_review.md
- if compliance review exists.

/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/09_tasks/09_traceability_matrix.md
/workflow/11_implementation_results/
- if final traceability validation requires source checks.
```

### Do Not Read By Default

```text
- raw chat history;
- raw agent scratchpads;
- superseded artifacts;
- rejected artifacts;
- unapproved draft outputs not referenced by Stage 12 artifacts;
- real secret values;
- unrelated source files.
```

## 4. USER_DIRECTIVES.md Handling

Check:

```text
/workflow/12_review_release_handoff/USER_DIRECTIVES.md
```

Apply final release/handoff directives. Report any conflicts with approved release scope, risk decisions, deployment expectations, or operations ownership.

## 5. Input Preflight Procedure

```text
[ ] Confirm all prior Stage 12 sub-SKILL artifacts exist or are explicitly N/A.
[ ] Verify required Stage 12 artifacts are not superseded or rejected.
[ ] Check code review findings.
[ ] Check security/privacy findings.
[ ] Check release/deployment readiness findings.
[ ] Check operations/documentation findings.
[ ] Identify all blockers, warnings, suggestions, accepted limitation candidates, assumptions, and open questions.
[ ] Identify conditional artifacts that were not created and need N/A records.
[ ] Identify traceability gaps.
[ ] Identify whether human approval can be requested or whether blockers prevent meaningful release decision.
```

Blocking preflight issues:

```text
- missing 12_code_review.md;
- missing 12_security_privacy_review.md when security/privacy review is applicable;
- missing 12_release_readiness.md;
- missing 12_documentation_handoff.md;
- unresolved blocker not represented in release readiness;
- inconsistent status across sub-SKILL artifacts;
- deployment requested but no deployment artifact or N/A rationale exists.
```

## 6. Execution Procedure

### Step 1. Consolidate Stage 12 Outputs

Read and summarize:

```text
code review outcome
security/privacy review outcome
release/deployment readiness outcome
operations/documentation handoff outcome
conditional artifact status
```

### Step 2. Build Final Finding Register

Create a consolidated list of findings using these categories:

```text
Release Blocker
Security Blocker
Privacy Blocker
Operational Blocker
Documentation Blocker
Warning
Suggestion
Accepted Limitation Candidate
Open Question
Traceability Gap
```

Each finding must include:

```text
Finding ID
Source Artifact
Category
Severity
Affected Requirement / Task / Release Item
Evidence
Recommended Action
Human Decision Needed
```

### Step 3. Determine Overall Readiness Recommendation

Use one status:

```text
Ready for Human Approval
Ready with Warnings
Not Ready: Blockers Exist
Partial / Internal-Only Release Candidate
Insufficient Evidence
```

This is a recommendation only. It is not approval.

### Step 4. Prepare Decision Candidates

Prepare explicit decision candidates:

```text
release decision
deployment decision
migration decision
rollback/recovery decision
security/privacy risk acceptance
accepted limitations
operations owner
documentation handoff
```

### Step 5. Prepare N/A Records

For every conditional artifact not created, record:

```text
artifact
why_not_applicable
revisit_if
```

Conditional artifacts requiring N/A records if absent:

```text
12_deployment_plan.md
12_operations_runbook.md
12_release_notes.md
12_migration_readiness.md
12_incident_rollback_plan.md
12_compliance_review.md
```

### Step 6. Update Traceability

Update or prepare updates to:

```text
/workflow/context/TRACEABILITY_MATRIX.md
```

Only update if traceability links are introduced or changed.

Preserve stable IDs. Do not break previous IDs.

### Step 7. Update Context Files

Update or prepare updates to:

```text
/workflow/context/context_packet.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
```

Do not update `DECISIONS.md` unless explicit human approval exists.

### Step 8. Write `result.md`

Create final Stage 12 result.

### Step 9. Present Human Approval Gate

End with explicit release/handoff approval options.

## 7. Output Artifacts

### Mandatory Artifacts

```text
/workflow/12_review_release_handoff/result.md
/workflow/context/context_packet.md
```

### Conditional Context Updates

```text
/workflow/context/ASSUMPTIONS.md
- if working assumptions exist.

/workflow/context/OPEN_QUESTIONS.md
- if unresolved questions exist.

/workflow/context/REJECTED_OPTIONS.md
- if release/deployment/handoff options were rejected or superseded.

/workflow/context/TRACEABILITY_MATRIX.md
- if traceability links are introduced or changed.
```

No new project feature artifacts should be created.

## 8. Required Output Structure

### `result.md`

```markdown
# Result: 12 Review / Security / Release / Handoff

## 1. Task Summary
## 2. Inputs Used
## 3. Outputs Created or Updated
## 4. Release Candidate Reviewed
## 5. Overall Release Readiness Status
## 6. Consolidated Finding Register
## 7. Blockers
## 8. Warnings
## 9. Suggestions
## 10. Security / Privacy Findings Summary
## 11. Deployment / Operations Findings Summary
## 12. Documentation Findings Summary
## 13. Accepted Limitation Candidates
## 14. Decision Candidates
## 15. Working Assumptions
## 16. Open Questions
## 17. N/A Records
## 18. Traceability Updates
## 19. Context Packet Updates
## 20. Human Approval Required
## 21. Recommended Next Step
```

### `context_packet.md`

Prepare Stage 13 context using:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 12 Review / Security / Release / Handoff
- Completed stages:
- Next recommended stage: 13 Workflow Retrospective & Skill Improvement

## 2. Approved Decisions
- Only human-approved release, deployment, operations, or handoff decisions.

## 3. Working Assumptions
- Release, deployment, security, privacy, operations, documentation, or retrospective assumptions not yet confirmed.

## 4. Open Questions
- Questions that may affect release, deployment, operation, documentation, or retrospective.

## 5. Rejected / Superseded Options
- Options that should not be reused unless reopened.

## 6. Constraints That Must Not Be Violated
- Scope:
- Security:
- Privacy:
- Deployment:
- Operations:
- Documentation:

## 7. Key Context for Next Stage
- Release readiness result.
- Review quality notes.
- Evidence quality notes.
- Agent failure patterns observed.
- Human judgment points.
- Skill/template improvement candidates.

## 8. Required Inputs for Next Stage
- /workflow/12_review_release_handoff/result.md
- /workflow/12_review_release_handoff/12_release_readiness.md
- /workflow/12_review_release_handoff/12_code_review.md
- /workflow/12_review_release_handoff/12_security_privacy_review.md
- /workflow/12_review_release_handoff/12_documentation_handoff.md
- conditional Stage 12 artifacts if created.

## 9. Do Not Do
- Do not treat release as approved unless the human explicitly approved it.
- Do not treat warnings as resolved unless evidence exists.
- Do not reopen rejected options unless the human explicitly reopens them.
```

## 9. Traceability Requirements

Preserve or update links:

```text
Goal
→ Requirement
→ Acceptance Criteria
→ Release Scope
→ Task
→ Implementation Evidence
→ Test Evidence
→ Review Finding
→ Release Decision Candidate
```

Record traceability gaps explicitly.

## 10. Validation Checklist

```text
[ ] All mandatory Stage 12 artifacts were read or missing status was reported.
[ ] Conditional artifacts were read or N/A records were prepared.
[ ] Code review findings were consolidated.
[ ] Security/privacy findings were consolidated.
[ ] Release/deployment findings were consolidated.
[ ] Operations/documentation findings were consolidated.
[ ] Blockers, warnings, suggestions, accepted limitation candidates, assumptions, and open questions were separated.
[ ] Overall release readiness recommendation was marked as recommendation, not approval.
[ ] Human approval gate was prepared.
[ ] context_packet.md was prepared for Stage 13.
[ ] DECISIONS.md was not updated without explicit human approval.
[ ] Secret values were not exposed.
```

## 11. Human Approval Gate

End with:

```markdown
## Human Approval Required

### Release Decision to Approve
- [ ] Approve release as ready.
- [ ] Approve release with warnings.
- [ ] Approve internal-only or staging-only release.
- [ ] Reject release until blockers are resolved.
- [ ] Defer release decision.

### Deployment Decision to Approve
- [ ] Approve deployment plan.
- [ ] Approve rollback plan.
- [ ] Approve migration plan, if applicable.
- [ ] Approve environment readiness.

### Security / Privacy Decisions to Approve
- [ ] Accept or reject listed security warnings.
- [ ] Accept or reject listed privacy warnings.
- [ ] Confirm no unresolved blocker remains.
- [ ] Accept or reject risk acceptance candidates.

### Operations / Handoff Decisions to Approve
- [ ] Approve operations owner.
- [ ] Approve handoff documentation.
- [ ] Approve support and escalation expectations.

### Accepted Limitations to Approve
- ...

### Assumptions to Confirm
- ...

### Open Questions to Resolve
- ...

### Artifacts Ready for Review
- /workflow/12_review_release_handoff/12_code_review.md
- /workflow/12_review_release_handoff/12_security_privacy_review.md
- /workflow/12_review_release_handoff/12_release_readiness.md
- /workflow/12_review_release_handoff/12_documentation_handoff.md
- /workflow/12_review_release_handoff/result.md
- conditional artifacts created during Stage 12

### Recommended Next Step
- If release is approved or rejected with lessons to capture, run Stage 13 Workflow Retrospective & Skill Improvement.
```

## 12. Next Stage Handoff

Next stage:

```text
/skills/13_retrospective/SKILL.md
```

Stage 13 should read only approved or clearly labeled Stage 12 artifacts and context files. It should not depend on Stage 12 internal sub-SKILL folders.

## Decision / Assumption / Open Question Rules

Use these classifications consistently:

```text
Approved Decision
- Only explicit human approval may create this.

Decision Candidate
- A recommended release, security, deployment, operations, or documentation decision awaiting human approval.

Working Assumption
- A temporary belief used only to continue safe partial work.

Open Question
- An unresolved issue that may affect release, deployment, security, privacy, operations, documentation, or retrospective.

Rejected Option
- An option explicitly rejected or superseded. Do not revive it unless the human reopens it.

Recommendation
- Agent advice. It is not a decision.
```

Do not update `DECISIONS.md` unless explicit human approval exists.

## Failure Handling

If the SKILL cannot be completed safely, create a partial output with:

```markdown
## Blocker Report

### Blocking Issue
- ...

### Why It Matters
- ...

### Affected Artifacts or Stages
- ...

### Safe Partial Work Completed
- ...

### Human Decision Needed
- ...
```

Do not pretend completion when required evidence is missing.

## Do Not Do

The agent must not:

- approve release, deployment, or risk acceptance on behalf of the human developer;
- silently turn assumptions into decisions;
- treat unapproved drafts as source of truth;
- use superseded or rejected artifacts as current truth;
- expose secret values;
- claim tests passed without evidence;
- mark a blocker as resolved without evidence;
- update `DECISIONS.md` without explicit human approval;
- create README.md or artifact_contract.yml unless explicitly requested.
