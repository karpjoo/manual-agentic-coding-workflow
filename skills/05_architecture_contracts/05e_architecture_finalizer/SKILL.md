---
name: 05e_architecture_finalizer
description: Consolidate Stage 5 architecture artifacts, finalize traceability, update context handoff, and prepare human approval gate.
stage: 05 Architecture & Technical Contracts
parent_skill: /skills/05_architecture_contracts/SKILL.md
subskill_id: 05e
subskill_order: 5
previous_subskill: /skills/05_architecture_contracts/05d_auth_security_operations/SKILL.md
next_subskill: /skills/06_data_design/SKILL.md
version: 1.0.0
status: draft
primary_output: /workflow/05_architecture/result.md
requires_human_approval: true
external_visibility: internal
---

# 05e Architecture Finalizer

## 1. Purpose

Use this sub-skill to consolidate Stage 5 official artifacts, detect contradictions, finalize traceability, prepare Stage 6 Data Design handoff, and present the human approval gate.

This finalizer does not make architecture decisions automatically approved. It prepares the official Stage 5 artifacts for human review.

## 2. When to Use

Use this sub-skill after:

```text
05a_architecture_drivers_options
05b_system_module_boundaries
05c_technical_contracts
05d_auth_security_operations
```

have completed, or after the human developer explicitly instructs the agent to finalize available Stage 5 partial outputs.

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
/workflow/03_requirements/03_traceability_matrix.md
/workflow/04_domain/04_domain_model.md
/workflow/04_domain/04_bounded_contexts.md
/workflow/04_domain/04_business_rules_invariants.md
/workflow/04_domain/04_domain_events.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md
```

### Read If Applicable

```text
/workflow/05_architecture/05_api_contracts.md
- if APIs or programmatic interfaces exist.

/workflow/05_architecture/05_integration_contracts.md
- if external integrations exist.

/workflow/05_architecture/05_event_contracts.md
- if events, async workflows, background jobs, queues, pub/sub, webhooks, or notifications exist.

/workflow/05_architecture/05_authn_authz_model.md
- if accounts, roles, permissions, protected resources, administrators, or protected operations exist.

/workflow/05_architecture/05_security_privacy_architecture.md
- if personal data, sensitive data, external data transfer, compliance concerns, LLM/API exposure, or security-sensitive workflows exist.

/workflow/05_architecture/05_operational_architecture.md
- if deployment, hosting, reliability, observability, environment management, secrets, background jobs, scaling, or operations are significant architecture concerns.

/workflow/05_architecture/05_brownfield_compatibility_plan.md
- if the project is brownfield, migration, compatibility-sensitive, or existing-system extension work.

/workflow/00_intake/00_existing_context_review.md
- if brownfield compatibility must be checked against existing system constraints.
```

### Do Not Read By Default

```text
- sub-skill SKILL.md files as source of project truth
- raw prompt history
- raw agent logs
- unapproved internal notes
- future Stage 6+ artifacts
- implementation source code unless final consistency review requires targeted brownfield verification
```

## 4. USER_DIRECTIVES.md Handling

If this file exists, read it before finalizing:

```text
/workflow/05_architecture/USER_DIRECTIVES.md
```

Apply stage-local directives. If directives conflict with approved decisions or existing Stage 5 artifacts, report the conflict and avoid silent overwrite.

## 5. Input Preflight Procedure

Verify:

```text
[ ] mandatory Stage 5 artifacts exist or missing artifacts are reported.
[ ] conditional Stage 5 artifacts were created or N/A rationale exists.
[ ] source artifacts are approved or explicitly allowed as draft inputs.
[ ] no superseded/rejected artifact is used as current truth.
[ ] architecture decisions are not falsely marked as approved.
[ ] traceability can be completed or gaps are recorded.
[ ] Stage 6 Data Design handoff can be prepared.
```

## 6. Missing Input Handling

Blocking issues:

```text
- missing architecture plan
- missing module boundaries
- missing architecture decisions
- required conditional artifact is missing with no N/A rationale
- unresolved conflict among architecture plan, module boundaries, contracts, auth/security, or operations artifacts
- unresolved security/privacy issue that affects architecture approval
- missing required input for Stage 6 handoff
```

If blocked, produce a partial `result.md` with a Blocker Report.

## 7. Execution Procedure

### Step 1. Inventory Stage 5 Artifacts

List:

```text
- mandatory artifacts found
- mandatory artifacts missing
- conditional artifacts created
- conditional artifacts marked N/A
- artifacts that are draft, approved, needs review, superseded, or conflicting
```

### Step 2. Check Consistency Across Artifacts

Check that:

```text
- architecture plan matches module boundaries
- module boundaries support requirements and domain model
- API contracts map to modules and protected operations
- integration contracts map to external systems and data flows
- event contracts map to domain events or async workflows
- auth model covers protected resources and operations
- security/privacy architecture covers identified risks and sensitive data flows
- operational architecture covers relevant runtime and observability concerns
- architecture decisions reflect options and trade-offs in artifacts
```

Record contradictions or gaps.

### Step 3. Finalize Architecture Traceability

Create or update:

```text
/workflow/05_architecture/05_architecture_traceability_matrix.md
```

Trace:

```text
Requirement
→ Acceptance Criteria
→ Domain Concept / Invariant / Event
→ Architecture Component / Module
→ API Contract / Integration Contract / Event Contract
→ Auth/Security/Operational Policy
→ Data Design Implication
→ Test Strategy Implication
```

### Step 4. Consolidate Architecture Decisions

Review and normalize:

```text
/workflow/05_architecture/05_architecture_decisions.md
```

Ensure:

```text
- every decision has a stable ID
- status is Proposed / Approved / Rejected / Superseded
- only explicit human approval creates Approved status
- rejected/superseded options are recorded clearly
- decision consequences and risks are explicit
- decision candidates are listed for human approval
```

### Step 5. Prepare Stage 6 Data Design Handoff

Extract for Stage 6:

```text
- architecture style relevant to data design
- module data ownership boundaries
- conceptual persistence needs
- query patterns implied by contracts
- access control implications
- audit logging implications
- external data transfer implications
- retention/deletion implications
- consistency/transaction boundaries
- background job or event persistence implications
- brownfield migration implications if applicable
- data design open questions
```

Do not create detailed data schema.

### Step 6. Update Workflow Context Files

Update or prepare:

```text
/workflow/context/context_packet.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
```

Do not update `DECISIONS.md` unless explicit human approval exists.

### Step 7. Create Stage Result

Create or update:

```text
/workflow/05_architecture/result.md
```

### Step 8. Present Human Approval Gate

List decisions, assumptions, open questions, risks, and artifacts ready for review.

## 8. Output Artifacts

### Mandatory Outputs

```text
/workflow/05_architecture/05_architecture_traceability_matrix.md
/workflow/05_architecture/result.md
/workflow/context/context_packet.md
```

### Mandatory Reviews / Updates

```text
/workflow/05_architecture/05_architecture_plan.md
/workflow/05_architecture/05_module_boundaries.md
/workflow/05_architecture/05_architecture_decisions.md
/workflow/context/TRACEABILITY_MATRIX.md
```

### Conditional Reviews

Review all conditional Stage 5 artifacts that exist or are applicable.

## 9. Required Output Structure

### 9.1 `05_architecture_traceability_matrix.md`

Use this structure:

```markdown
# 05 Architecture Traceability Matrix

## 1. Status
- Draft / Needs Review / Approved

## 2. Approved Inputs Used

## 3. Traceability Summary

## 4. Requirement to Architecture Mapping

| Requirement ID | Acceptance Criteria | Domain Concept | Architecture Component | Contract | Auth/Security/Operational Policy | Data Design Implication | Test Implication |
|---|---|---|---|---|---|---|---|

## 5. Domain to Architecture Mapping

| Domain Concept / Invariant / Event | Architecture Component | Contract / Policy | Notes |
|---|---|---|---|

## 6. Architecture Decision Mapping

| ADR ID | Related Requirements | Related Domain Concepts | Related Artifacts | Stage 6 Implication |
|---|---|---|---|---|

## 7. Traceability Gaps

## 8. Human Approval Required
```

### 9.2 `result.md`

Use this structure:

```markdown
# Result: 05 Architecture & Technical Contracts

## 1. Task Summary

## 2. Inputs Used

## 3. Outputs Created or Updated

## 4. Approved Decisions Used

## 5. Architecture Summary

## 6. New Decision Candidates

## 7. Working Assumptions

## 8. Open Questions

## 9. Risks and Constraints

## 10. Rejected or Superseded Options

## 11. Traceability Updates

## 12. N/A Items

| Artifact | Why Not Applicable | Revisit If |
|---|---|---|

## 13. Stage 6 Data Design Handoff

## 14. Validation Checklist Result

## 15. Human Approval Required

### Decisions to Approve

### Assumptions to Confirm

### Open Questions to Resolve

### Risks to Review

### Artifacts Ready for Review

## 16. Recommended Next Step
```

### 9.3 `context_packet.md`

Update with minimal context for Stage 6:

```markdown
# context_packet.md

## 1. Current Project State
- Current stage: 05_architecture_contracts
- Completed stages:
- Next recommended stage: 06_data_design

## 2. Approved Decisions
- Only human-approved decisions relevant to Stage 6.

## 3. Working Assumptions
- Architecture assumptions that Stage 6 must be aware of.

## 4. Open Questions
- Questions affecting data design, security rules, schema, query patterns, migration, or data lifecycle.

## 5. Rejected / Superseded Options
- Architecture or technology options not to revive unless reopened.

## 6. Constraints That Must Not Be Violated
- Technology constraints
- Security constraints
- Privacy constraints
- Scope constraints
- Operational constraints

## 7. Key Context for Next Stage
- Architecture style
- Module boundaries
- Contract boundaries
- Data ownership implications
- Auth/access implications
- Integration implications
- Event/async implications
- Audit/logging implications
- Consistency/transaction implications

## 8. Required Inputs for Next Stage
- /workflow/05_architecture/05_architecture_plan.md
- /workflow/05_architecture/05_module_boundaries.md
- /workflow/05_architecture/05_architecture_decisions.md
- /workflow/05_architecture/05_architecture_traceability_matrix.md
- Conditional Stage 5 artifacts that were created and approved
- /workflow/03_requirements/03_requirements.md
- /workflow/03_requirements/03_acceptance_criteria.md
- /workflow/04_domain/04_domain_model.md
- /workflow/04_domain/04_business_rules_invariants.md

## 9. Do Not Do
- Do not design schema from unapproved architecture.
- Do not ignore auth/access rules when designing data.
- Do not treat architecture recommendations as approved decisions.
- Do not use internal sub-skill outputs as source of truth.
```

## 10. Traceability Rules

Use stable IDs:

```text
ARC-001, ARC-002
MOD-001, MOD-002
API-001, API-002
INT-001, INT-002
EVT-001, EVT-002
AUTHZ-001, AUTHZ-002
SEC-001, SEC-002
OPS-001, OPS-002
ADR-001, ADR-002
```

Rules:

```text
- Do not break existing requirement IDs.
- Do not rename domain concept IDs without explanation.
- Every major architecture component must link to a requirement, domain concept, risk, or operational constraint.
- Every API/integration/event contract must link to a requirement or domain workflow.
- If traceability cannot be completed, record the gap.
```

## 11. Decision / Assumption / Open Question Rules

- Only explicit human approval creates approved decisions.
- Architecture decision candidates remain proposed until approved.
- Working assumptions must not be copied into approved decisions.
- Open questions must be preserved if they affect Stage 6 or later stages.
- Rejected options must not be revived unless the human explicitly reopens them.

## 12. Validation Checklist

```text
[ ] Mandatory Stage 5 artifacts exist or missing artifacts are reported.
[ ] Conditional artifacts were created or N/A rationale was recorded.
[ ] Architecture plan and module boundaries are consistent.
[ ] Contracts are consistent with modules and requirements.
[ ] Auth/security/operations artifacts are consistent with risk/privacy screening.
[ ] Architecture decisions are correctly marked Proposed/Approved/Rejected/Superseded.
[ ] Traceability matrix was created or updated.
[ ] Stage 6 Data Design handoff was prepared.
[ ] context_packet.md was updated as navigation layer only.
[ ] Assumptions, open questions, risks, and recommendations are separated.
[ ] Human approval gate is explicit.
```

## 13. Human Approval Gate

Stage 5 must end with:

```markdown
## Human Approval Required

### Decisions to Approve
- Architecture style and direction
- Major technical choices
- Frontend/backend/service boundary
- Module boundaries
- API contracts, if applicable
- Integration contracts, if applicable
- Authentication and authorization model, if applicable
- Event/async contracts, if applicable
- Security/privacy architecture direction, if applicable
- Operational architecture direction, if applicable

### Assumptions to Confirm
- Technology stack assumptions
- Deployment/hosting assumptions
- Integration availability assumptions
- Performance/scalability assumptions
- Auth provider assumptions
- Data ownership assumptions
- Observability/logging assumptions

### Open Questions to Resolve
- Architecture questions affecting Stage 6 Data Design
- Contract questions affecting Stage 8 Test Strategy
- Security/privacy questions affecting implementation safety
- Operational questions affecting deployment or release

### Risks to Review
- Architecture complexity risks
- Security/privacy risks
- Data consistency risks
- Integration reliability risks
- Vendor lock-in risks
- Maintainability risks
- Testability risks

### Artifacts Ready for Review
- /workflow/05_architecture/05_architecture_plan.md
- /workflow/05_architecture/05_module_boundaries.md
- /workflow/05_architecture/05_architecture_decisions.md
- /workflow/05_architecture/05_architecture_traceability_matrix.md
- /workflow/05_architecture/result.md
- Conditional artifacts created for this project

### Recommended Next Step
- Human reviews Stage 5 artifacts.
- After explicit approval, proceed to Stage 6 Data Design.
```

## 14. Do Not Do

Do not:

- approve architecture decisions yourself
- update `DECISIONS.md` without explicit human approval
- hide contradictions among artifacts
- treat missing conditional artifacts as N/A without rationale
- create detailed data schema
- create task cards
- create implementation prompts
- rely on internal sub-skill files as project truth
- make Stage 6 depend on unapproved Stage 5 artifacts
- omit Stage 6 handoff context
