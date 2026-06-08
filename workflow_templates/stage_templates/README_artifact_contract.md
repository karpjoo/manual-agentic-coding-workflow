# Prompt: Create `README.md` and `artifact_contract.yml` for a Reusable SKILL

## Purpose

Use this prompt to create support files for a reusable `SKILL.md` in a Manual Agentic Coding Workflow.

This prompt creates:

* `README.md`
* `artifact_contract.yml`

It does **not** execute the SKILL.
It does **not** create project artifacts under `/workflow`.

---

## Target Stage Information

Fill in the following values before running this prompt.

```text
Stage number: [[FILL: stage number, e.g. 01]]
Stage name: [[FILL: stage name, e.g. service_goal_definition]]
Human-readable stage title: [[FILL: e.g. Service Goal Definition]]

SKILL folder: [[FILL: e.g. /skills/01_service_goal_definition]]
SKILL file: [[FILL: e.g. /skills/01_service_goal_definition/SKILL.md]]

Stage template file: [[FILL: e.g. /workflow_templates/stage_templates/01_service_goal_skill_template.md, if available]]

Primary project artifact: [[FILL: e.g. /workflow/01_goal/01_service_goal.md]]
Stage result artifact: [[FILL: e.g. /workflow/01_goal/result.md]]

Previous stage: [[FILL: e.g. 00_project_intake]]
Next stage: [[FILL: e.g. 02_stakeholder_risk_framing]]
```

---

## Prompt

You are creating support files for a reusable SKILL in a Manual Agentic Coding Workflow.

Your task is to create **ONLY** the support files for the target reusable SKILL.

## Target Stage

* Stage number: `[[FILL: stage number]]`
* Stage name: `[[FILL: stage name]]`
* Human-readable stage title: `[[FILL: human-readable stage title]]`
* SKILL folder: `[[FILL: SKILL folder]]`
* SKILL file: `[[FILL: SKILL file]]`
* Stage template file: `[[FILL: Stage template file, if available]]`
* Primary project artifact: `[[FILL: Primary project artifact]]`
* Stage result artifact: `[[FILL: Stage result artifact]]`
* Previous stage: `[[FILL: Previous stage]]`
* Next stage: `[[FILL: Next stage]]`

## Target Output Files

Create **ONLY** these files:

```text
[[FILL: SKILL folder]]/README.md
[[FILL: SKILL folder]]/artifact_contract.yml
```

## Do Not Do

Do **NOT** execute the SKILL.

Do **NOT** create project artifacts under `/workflow`.

Do **NOT** create or modify:

```text
[[FILL: Primary project artifact]]
[[FILL: Stage result artifact]]
```

Do **NOT** create project-specific assumptions, product ideas, user groups, architecture, database, UI, test plans, implementation tasks, or code.

Do **NOT** change the `SKILL.md` content unless explicitly instructed.

Do **NOT** treat this task as a workflow stage execution.

---

## Source Documents

Use the following source documents when available:

```text
[[FILL: SKILL file]]
[[FILL: Stage template file, if available]]
/workflow_templates/core/core_skill_template.md
agentic-coding-workflow-concept-and-design.md
skill-template-design-principles.md
workflow_folder_structure_guide.md
```

Also use these if provided:

```text
/workflow_templates/specializations/[[FILL: specialization addendum, if applicable]]
/workflow_templates/tool_wrappers/[[FILL: tool wrapper, if applicable]]
```

If any source document is missing:

1. Report it under `Missing or Unavailable Inputs`.
2. Decide whether it is blocking.
3. Continue if the missing document is not blocking.
4. Do not invent stage-specific rules that should come from a missing `SKILL.md`.

---

## Important Distinction

* `README.md` is a human-facing usage guide.
* `artifact_contract.yml` is a structured contract for validation, consistency checking, and automation.
* Neither file is an executable SKILL.
* Neither file is a project artifact.
* Both files must remain reusable across projects.

---

# File 1: `README.md`

Create a concise but useful `README.md` for human developers who want to use this SKILL.

## README Requirements

The `README.md` must include:

1. Title
2. What this SKILL is for
3. When to use it
4. When not to use it
5. Required inputs before running
6. Optional or conditional inputs
7. Outputs created when the SKILL is executed
8. Human approval requirements
9. How to run the SKILL in an Agentic Coding tool
10. Relationship to previous and next stages
11. How to interpret `Draft`, `Approved`, and `Needs Review`
12. Common mistakes to avoid
13. Troubleshooting / blocker cases
14. Recommended next step after successful execution

## README Style Rules

* Write for experienced human developers.
* Be practical and concise.
* Do not repeat the full `SKILL.md`.
* Do not include long theoretical explanations.
* Do not include project-specific examples unless they are clearly marked as placeholders.
* Clearly distinguish reusable SKILL files from project execution artifacts.
* Make clear that human approval is required before downstream stages rely on approved decisions.

---

# File 2: `artifact_contract.yml`

Create a machine-readable `artifact_contract.yml`.

The YAML must be valid and reusable across projects.

## Required YAML Structure

Use this structure:

```yaml
contract_version: "1.0.0"

skill:
  name: "[[FILL from SKILL.md]]"
  stage: "[[FILL: stage number and name]]"
  title: "[[FILL: human-readable stage title]]"
  skill_path: "[[FILL: SKILL file]]"
  readme_path: "[[FILL: SKILL folder]]/README.md"
  primary_output: "[[FILL: Primary project artifact]]"
  requires_human_approval: true

purpose:
  summary: "[[FILL: concise summary of what this SKILL does]]"
  core_question: "[[FILL: central question this stage answers]]"

input_contract:
  always_read:
    - path: "[[FILL]]"
      required: true
      purpose: "[[FILL]]"
      source_of_truth: true
      approval_required: false

  read_if_applicable:
    - path: "[[FILL]]"
      condition: "[[FILL]]"
      purpose: "[[FILL]]"

  do_not_read_by_default:
    - path_or_pattern: "[[FILL]]"
      reason: "[[FILL]]"

  missing_input_handling:
    missing_required_input: "[[FILL]]"
    missing_stage_input: "[[FILL]]"
    no_project_context: "[[FILL]]"
    conflicting_inputs: "[[FILL]]"
    draft_or_unapproved_inputs: "[[FILL]]"

user_directives:
  path: "[[FILL: stage-local USER_DIRECTIVES.md path]]"
  required_if_exists: true
  handling_rules:
    - "Read before executing the SKILL."
    - "Classify directives as approval, correction, preference, rejection, scope change, constraint, question, or new input."
    - "Do not treat every directive as a globally approved decision."
    - "Report conflicts with approved decisions."

output_contract:
  mandatory_artifacts:
    - path: "[[FILL: mandatory artifact path]]"
      purpose: "[[FILL]]"
      required: true
      approval_required: true
      status_values:
        - Draft
        - Approved
        - Needs Review
      required_sections:
        - "[[FILL]]"

  conditional_artifacts:
    - path: "[[FILL: conditional artifact path]]"
      condition: "[[FILL]]"
      purpose: "[[FILL]]"
      n_a_record_required: true

  n_a_record:
    required: true
    required_fields:
      - artifact
      - why_not_applicable
      - revisit_if

context_updates:
  files_to_update:
    - path: "/workflow/context/context_packet.md"
      condition: "Always update or prepare for the next stage."
      update_rule: "Include only the minimum operational context needed by the next stage."

    - path: "/workflow/context/ASSUMPTIONS.md"
      condition: "Update if working assumptions exist."
      update_rule: "Record assumptions without treating them as decisions."

    - path: "/workflow/context/OPEN_QUESTIONS.md"
      condition: "Update if unresolved questions exist."
      update_rule: "Record questions that may affect later stages."

    - path: "/workflow/context/REJECTED_OPTIONS.md"
      condition: "Update if options were explicitly rejected or superseded."
      update_rule: "Do not revive rejected options unless explicitly reopened."

    - path: "/workflow/context/TRACEABILITY_MATRIX.md"
      condition: "Update if traceability links are introduced or changed."
      update_rule: "Use stable IDs and preserve existing links."

  context_packet:
    path: "/workflow/context/context_packet.md"
    purpose: "Prepare minimal context for the next stage."
    next_stage: "[[FILL: Next stage]]"
    required_sections:
      - Current Project State
      - Approved Decisions
      - Working Assumptions
      - Open Questions
      - Rejected / Superseded Options
      - Constraints That Must Not Be Violated
      - Key Context for Next Stage
      - Required Inputs for Next Stage
      - Do Not Do

traceability:
  id_conventions:
    goals: "G-001, G-002"
    assumptions: "A-001, A-002"
    questions: "Q-001, Q-002"
    risks: "R-001, R-002"
    requirements: "REQ-001, REQ-002"
    tasks: "TASK-001, TASK-002"

  required_links:
    - "[[FILL: stage-specific traceability link]]"

  prohibited_links:
    - "[[FILL: links this stage must not create prematurely]]"

classification_rules:
  approved_decision:
    rule: "Only explicit human approval can create an approved decision."
    examples:
      - "[[FILL: stage-specific example]]"

  decision_candidate:
    rule: "Agent recommendations awaiting human approval must be marked as decision candidates."

  working_assumption:
    rule: "Temporary beliefs needed for progress must remain assumptions until confirmed."

  open_question:
    rule: "Unresolved issues that may affect later work must be recorded as open questions."

  rejected_option:
    rule: "Explicitly rejected or superseded options must be recorded and not revived unless reopened."

  recommendation:
    rule: "Recommendations are not decisions and must not be recorded as approved."

approval_gate:
  required: true
  decisions_to_approve:
    - "[[FILL: stage-specific decision requiring approval]]"
  assumptions_to_confirm:
    - "[[FILL]]"
  open_questions_to_resolve:
    - "[[FILL]]"
  risks_to_review:
    - "[[FILL]]"
  artifacts_ready_for_review:
    - "[[FILL: Primary project artifact]]"
    - "[[FILL: Stage result artifact]]"

validation:
  checklist:
    - "[[FILL: stage-specific validation item]]"

  failure_conditions:
    - "[[FILL: stage-specific failure condition]]"

  blocker_report_required: true
  blocker_report_fields:
    - blocking_issue
    - why_it_matters
    - affected_artifacts_or_stages
    - safe_partial_work_completed
    - human_decision_needed

prohibited_actions:
  - "[[FILL: stage-specific prohibited action]]"

specialization_hooks:
  allowed: true
  examples:
    - name: web_saas
      may_add:
        - additional inputs
        - additional questions
        - conditional artifacts
        - validation concerns

    - name: internal_tool
      may_add:
        - workflow value questions
        - operator value questions
        - organizational constraints

    - name: mobile_app
      may_add:
        - device context questions
        - platform constraints
        - offline or permission concerns

    - name: ai_data_product
      may_add:
        - data source questions
        - evaluation purpose
        - model output value
        - human review concerns

    - name: regulated_security_sensitive
      may_add:
        - compliance constraints
        - privacy-sensitive questions
        - audit or risk boundaries

    - name: brownfield_legacy
      may_add:
        - migration constraints
        - compatibility constraints
        - existing-system review inputs

  must_not_change:
    - approval_rules
    - artifact_contract
    - assumption_handling
    - traceability_rules
    - stage_boundaries

tool_wrapper_hooks:
  allowed:
    - file_creation_commands
    - save_locations
    - sandbox_rules
    - review_workflow
    - command_invocation_conventions

  must_not_change:
    - stage_reasoning
    - approval_rules
    - artifact_contract
    - assumption_handling
    - traceability_rules
    - stage_boundaries
```

## YAML Rules

* Use valid YAML.
* Use stable keys.
* Prefer explicit lists over long prose.
* Keep descriptions short.
* Do not include markdown headings inside YAML values unless necessary.
* Do not include project-specific content.
* Do not include executable shell commands unless generic and optional.
* Do not include downstream artifacts unless required as handoff references or explicitly defined by the SKILL.
* Include `status_values` where applicable.
* Include N/A rules for conditional artifacts.

---

## Consistency Check

Before returning the files, verify:

1. `README.md` and `artifact_contract.yml` agree with `SKILL.md`.
2. Mandatory artifacts match the SKILL.
3. Conditional artifacts match the SKILL.
4. Input rules match the SKILL.
5. Missing input handling matches the SKILL.
6. Human approval rules match the SKILL.
7. Context handoff rules match the SKILL.
8. Do-not-do rules match the SKILL.
9. No project-specific content was introduced.
10. No `/workflow` project artifact was created.

---

## Output Format

Return the complete content of both files as separate fenced code blocks:

1. `README.md`
2. `artifact_contract.yml`

After the code blocks, include a short `Design Notes` section with:

* source documents used
* missing or unavailable inputs
* key assumptions made
* why no project artifacts were created
* what should be done next
