---
name: 12d_operations_documentation_handoff
description: Prepare operations runbook and documentation handoff by reviewing runtime dependencies, monitoring, troubleshooting, ownership, setup docs, release notes, and known limitations.
stage: 12 Review / Security / Release / Handoff
parent_skill: /skills/12_review_release_handoff/SKILL.md
subskill_id: 12d
subskill_order: 4
previous_subskill: /skills/12_review_release_handoff/12c_release_deployment_readiness/SKILL.md
next_subskill: /skills/12_review_release_handoff/12e_review_release_finalizer/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/12_review_release_handoff/12_documentation_handoff.md
requires_human_approval: true
external_visibility: internal
---

# 12d Operations / Documentation Handoff

## 1. Purpose

This sub-SKILL prepares the operational and documentation handoff for the release candidate.

It reviews or drafts:

- operations runbook;
- runtime dependencies;
- configuration overview;
- monitoring/logging expectations;
- common failure modes;
- troubleshooting steps;
- incident response, rollback, and recovery notes;
- ownership and escalation;
- developer setup documentation;
- user/admin documentation;
- API/integration documentation;
- environment and deployment documentation;
- known limitations and release notes.

This sub-SKILL does not approve operations ownership or documentation handoff. It prepares artifacts for human review.

## 2. Core Question

```text
Can a human operator, maintainer, or future developer understand how to run, monitor, troubleshoot, support, and continue the released system using current documentation?
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

/workflow/07_mvp_release/07_mvp_scope.md
/workflow/08_test_strategy/08_validation_commands.md
/workflow/11_implementation_results/
/workflow/12_review_release_handoff/12_code_review.md
/workflow/12_review_release_handoff/12_security_privacy_review.md
/workflow/12_review_release_handoff/12_release_readiness.md
```

### Read If Applicable

```text
/workflow/05_architecture/05_architecture_plan.md
- if operators need system structure or runtime dependency context.

/workflow/05_architecture/05_integration_contracts.md
- if integrations affect operations or troubleshooting.

/workflow/06_data/06_migration_plan.md
- if migration or data repair information is needed.

/workflow/06_data/06_data_security_rules.md
- if access/security rules affect operation.

/workflow/12_review_release_handoff/12_deployment_plan.md
- if deployment is in scope.

/workflow/12_review_release_handoff/12_migration_readiness.md
- if migration is in scope.

/workflow/12_review_release_handoff/12_incident_rollback_plan.md
- if rollback/recovery has separate details.

/workflow/12_review_release_handoff/12_release_notes.md
- if release notes exist.

Project README, setup docs, API docs, admin docs, deployment docs, docs directory
- if available and relevant.

CI/deployment configuration and package scripts
- if needed to document run/test/deploy operations.
```

### Do Not Read By Default

```text
- raw chat history;
- private credentials;
- secret values;
- logs with personal/sensitive data;
- unrelated historical drafts;
- rejected documentation proposals.
```

## 4. USER_DIRECTIVES.md Handling

Check:

```text
/workflow/12_review_release_handoff/USER_DIRECTIVES.md
```

Apply directives related to operations owner, support process, documentation style, handoff recipient, release notes, or known limitations.

## 5. Input Preflight Procedure

```text
[ ] Identify whether operations handoff is needed.
[ ] Identify deployment target and release type.
[ ] Identify operators, maintainers, or handoff recipients if available.
[ ] Identify documents available for review.
[ ] Identify runtime dependencies.
[ ] Identify configuration requirements by name only.
[ ] Identify monitoring/logging expectations.
[ ] Identify known limitations and warnings from prior sub-SKILLs.
[ ] Identify open questions affecting operations or documentation.
```

Blocking preflight issues:

```text
- operations handoff required but no owner identified;
- deployment expected but no deployment/run documentation exists;
- known limitation affects users/operators but is undocumented;
- rollback/recovery required but not documented;
- secret handling documentation would require exposing secret values.
```

## 6. Execution Procedure

### Step 1. Confirm Handoff Scope

Record:

```text
handoff type: developer, operator, admin, user, client, internal team, production support
release target
expected maintenance owner
documents reviewed
documents missing
```

### Step 2. Prepare Operations Runbook if Applicable

Create or update:

```text
/workflow/12_review_release_handoff/12_operations_runbook.md
```

Include:

```text
system overview
runtime dependencies
configuration overview
monitoring/logging
common failure modes
troubleshooting steps
incident response
rollback/recovery
backup/export notes if applicable
ownership/escalation
maintenance notes
```

### Step 3. Review Documentation Freshness

Check:

```text
project README
developer setup
environment variable documentation
run/test commands
deployment instructions
API documentation
integration documentation
user/admin documentation
known limitations
release notes
migration notes
troubleshooting
```

### Step 4. Identify Documentation Gaps

Classify gaps as:

```text
Documentation Blocker
Warning
Suggestion
Not Applicable
```

A documentation blocker exists when release/handoff cannot be safely understood or operated without the missing documentation.

### Step 5. Check Claims Against Evidence

Documentation must not claim:

```text
features not implemented
security guarantees not reviewed
test coverage not evidenced
production readiness not approved
data handling policies not confirmed
```

### Step 6. Prepare Handoff Checklist

Include:

```text
artifacts ready for handoff
operator actions needed
documentation gaps
known limitations
open questions
human approvals required
next owner
```

## 7. Output Artifacts

### Mandatory Artifacts

```text
/workflow/12_review_release_handoff/12_documentation_handoff.md
```

### Conditional Artifacts

```text
/workflow/12_review_release_handoff/12_operations_runbook.md
- if the system will be operated, monitored, supported, deployed, maintained, or handed off.
```

If the conditional artifact is not created, record N/A rationale for finalizer.

## 8. Required Output Structure

### `12_documentation_handoff.md`

```markdown
# 12 Documentation Handoff

## 1. Documentation Scope
## 2. Inputs Reviewed
## 3. Documents Reviewed
## 4. Developer Setup Documentation
## 5. User / Admin Documentation
## 6. API / Integration Documentation
## 7. Environment and Deployment Documentation
## 8. Known Limitations Documentation
## 9. Release Notes Review
## 10. Documentation Gaps
## 11. Documentation Blockers
## 12. Warnings
## 13. Suggestions
## 14. Handoff Checklist
## 15. Human Approval Required
## 16. Handoff to 12e Finalizer
```

### `12_operations_runbook.md`

```markdown
# 12 Operations Runbook

## 1. System Overview
## 2. Runtime Dependencies
## 3. Configuration Overview
## 4. Monitoring and Logging
## 5. Common Failure Modes
## 6. Troubleshooting Steps
## 7. Incident Response
## 8. Rollback and Recovery
## 9. Data Backup / Export Notes
## 10. Ownership and Escalation
## 11. Maintenance Notes
```

## 9. Traceability Requirements

Preserve links:

```text
Release Scope → Operational Concern → Documentation Item → Handoff Status → Finding
```

Use IDs:

```text
OPS-001, OPS-002, ...
DOC-001, DOC-002, ...
```

## 10. Validation Checklist

```text
[ ] Handoff scope was identified.
[ ] Operations runbook was created if applicable.
[ ] Documentation freshness was reviewed.
[ ] Known limitations were checked against documentation.
[ ] Release notes were reviewed if applicable.
[ ] Documentation blockers, warnings, and suggestions were separated.
[ ] Secret values were not exposed.
[ ] Handoff checklist was prepared.
[ ] Handoff notes for finalizer were included.
```

## 11. Human Approval Gate

This sub-SKILL prepares operations and documentation handoff decision candidates.

End with:

```markdown
## Human Review Needed

### Operations Decisions
- ...

### Documentation Blockers
- ...

### Handoff Approval Candidates
- ...

### Open Questions
- ...

### Recommended Next Sub-SKILL
- Run `/skills/12_review_release_handoff/12e_review_release_finalizer/SKILL.md`.
```

## 12. Context Handoff to Finalizer

At the end of `12_documentation_handoff.md`, include:

```markdown
## Handoff to 12e Finalizer

### Documentation Blockers
### Operations Blockers
### Warnings
### Suggestions
### Accepted Limitation Candidates
### Open Questions
### Artifacts Ready for Final Review
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
