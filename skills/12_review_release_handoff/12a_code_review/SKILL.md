---
name: 12a_code_review
description: Review implemented release candidate against approved requirements, acceptance criteria, task evidence, code quality, architecture boundaries, and scope control.
stage: 12 Review / Security / Release / Handoff
parent_skill: /skills/12_review_release_handoff/SKILL.md
subskill_id: 12a
subskill_order: 1
previous_subskill: /skills/12_review_release_handoff/SKILL.md
next_subskill: /skills/12_review_release_handoff/12b_security_privacy_review/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/12_review_release_handoff/12_code_review.md
requires_human_approval: true
external_visibility: internal
---

# 12a Code Review

## 1. Purpose

This sub-SKILL reviews whether the implemented release candidate satisfies approved requirements and acceptance criteria, stays within approved scope, and meets release-level code quality expectations.

It focuses on:

- requirement satisfaction;
- acceptance criteria coverage;
- implementation evidence;
- test evidence references;
- code quality findings;
- architecture or module boundary drift;
- performance and reliability concerns;
- unnecessary scope expansion;
- release blockers, warnings, and suggestions.

This sub-SKILL does not perform implementation, refactoring, deployment, or release approval.

## 2. Core Question

```text
Does the implemented release candidate satisfy the approved scope with sufficient evidence and without code-quality, architecture, or scope-control issues that should block or warn against release?
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

/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/07_mvp_release/07_mvp_scope.md
/workflow/07_mvp_release/07_release_slices.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/09_tasks/09_task_cards.md
/workflow/09_tasks/09_traceability_matrix.md
/workflow/11_implementation_results/
```

### Read If Applicable

```text
/workflow/00_intake/00_existing_context_review.md
- if this is brownfield, migration, extension, or compatibility-sensitive.

/workflow/04_domain/04_business_rules_invariants.md
- if business rules, invariants, state transitions, or lifecycle rules affect correctness.

/workflow/05_architecture/05_architecture_plan.md
- if module boundaries, runtime structure, or architecture decisions affect review.

/workflow/05_architecture/05_api_contracts.md
- if APIs exist.

/workflow/05_architecture/05_integration_contracts.md
- if integrations exist.

/workflow/06_data/06_logical_schema.md
- if persistent data behavior affects correctness.

/workflow/11_implementation_results/11_task_result_*.md
- if task-level result files exist.

/workflow/11_implementation_results/11_test_evidence_*.md
- if task-level evidence files exist.

Relevant code files
- only if needed to verify implementation evidence, scope drift, or code quality findings.
```

### Do Not Read By Default

```text
- raw chat history;
- raw agent scratchpads;
- unrelated historical drafts;
- superseded artifacts;
- rejected artifacts;
- unrelated source files;
- real secret values.
```

## 4. USER_DIRECTIVES.md Handling

Check:

```text
/workflow/12_review_release_handoff/USER_DIRECTIVES.md
```

Apply stage-local human instructions before assumptions. If directives change release scope or contradict approved decisions, report a conflict.

## 5. Input Preflight Procedure

Before reviewing code:

```text
[ ] Confirm the release candidate or implemented task set under review.
[ ] Identify approved release scope.
[ ] Identify must-have requirements.
[ ] Identify task result files.
[ ] Identify test evidence files.
[ ] Check whether implementation evidence exists for each release-scoped task.
[ ] Check whether source artifacts are approved or clearly marked as draft.
[ ] Check for superseded/rejected artifacts.
[ ] Identify missing evidence, ambiguity, or conflicts.
```

Blocking preflight issues:

```text
- no approved release scope;
- no implementation evidence;
- no acceptance criteria;
- no task-to-requirement traceability;
- code review requested for unknown release candidate.
```

## 6. Execution Procedure

### Step 1. Confirm Review Scope

Record:

```text
release candidate or task set
approved release scope
excluded or deferred work
source artifacts reviewed
whether review is full, partial, internal-only, staging, or production-oriented
```

### Step 2. Build Requirement-to-Evidence Review Table

For each release-scoped requirement:

```text
Requirement ID
Acceptance Criteria
Linked Task IDs
Implementation Evidence
Test Evidence Reference
Code Review Status
Finding IDs
```

Status values:

```text
Covered
Partially Covered
Not Covered
Not Applicable
Blocked
Needs Human Decision
```

### Step 3. Review Requirement Satisfaction

Check each must-have requirement against implementation and evidence.

Do not mark a requirement satisfied unless evidence exists.

### Step 4. Review Code Quality

Check:

```text
unnecessary scope expansion
large or risky changes not tied to task cards
duplicated or dead code
temporary TODOs that affect release
unclear error handling
fragile boundary checks
excessive coupling
performance-sensitive paths
reliability concerns
dependency changes
logging and observability gaps
```

### Step 5. Review Architecture and Boundary Drift

If architecture artifacts exist, check whether implementation drifted from:

```text
module boundaries
API contracts
integration contracts
auth/authz flow
data ownership boundaries
error handling policy
observability policy
```

### Step 6. Classify Findings

Classify each finding as:

```text
Release Blocker
Warning
Suggestion
Accepted Limitation Candidate
Open Question
```

Each finding must include:

```text
Finding ID
Severity
Affected Requirement / Task / File / Artifact
Evidence
Impact
Recommended Action
Human Decision Needed
```

### Step 7. Write `12_code_review.md`

Use the required structure below.

## 7. Output Artifacts

### Mandatory Artifacts

```text
/workflow/12_review_release_handoff/12_code_review.md
```

### Conditional Artifacts

None for this sub-SKILL. If additional review notes are needed, include them inside `12_code_review.md`.

## 8. Required Output Structure

```markdown
# 12 Code Review

## 1. Review Scope
## 2. Inputs Reviewed
## 3. Requirement Satisfaction Review
## 4. Requirement-to-Evidence Matrix
## 5. Code Quality Findings
## 6. Architecture / Module Boundary Findings
## 7. Performance and Reliability Findings
## 8. Unnecessary Scope Expansion
## 9. Blockers
## 10. Warnings
## 11. Suggestions
## 12. Accepted Limitation Candidates
## 13. Open Questions
## 14. Evidence References
## 15. Review Conclusion
## 16. Handoff to 12b Security / Privacy Review
```

## 9. Traceability Requirements

Preserve links:

```text
Requirement → Acceptance Criteria → Release Scope → Task → Implementation Evidence → Test Evidence → Review Finding
```

Use finding IDs:

```text
REV-001, REV-002, ...
```

## 10. Validation Checklist

```text
[ ] Approved release scope was identified.
[ ] Must-have requirements were reviewed.
[ ] Acceptance criteria were checked.
[ ] Implementation evidence was reviewed.
[ ] Test evidence references were recorded.
[ ] Code quality findings were classified.
[ ] Architecture/boundary drift was checked when applicable.
[ ] Blockers, warnings, suggestions, and accepted limitation candidates were separated.
[ ] Open questions were recorded.
[ ] Handoff notes for 12b were included.
```

## 11. Human Approval Gate

This sub-SKILL does not approve release. It prepares findings for later finalization.

End with:

```markdown
## Human Review Needed

### Code Review Blockers
- ...

### Warnings
- ...

### Accepted Limitation Candidates
- ...

### Open Questions
- ...

### Recommended Next Sub-SKILL
- Run `/skills/12_review_release_handoff/12b_security_privacy_review/SKILL.md`.
```

## 12. Context Handoff to Next Sub-SKILL

At the end of `12_code_review.md`, include a concise handoff section for 12b:

```markdown
## Handoff to 12b Security / Privacy Review

### Security-Relevant Code Findings
### Privacy-Relevant Code Findings
### Auth / Permission Areas to Inspect
### Data Handling Areas to Inspect
### Open Questions Affecting Security or Privacy
```

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
