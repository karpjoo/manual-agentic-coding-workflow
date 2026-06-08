# Stage 0 Project Intake Skill

This folder contains the reusable skill for Stage 0 of the Manual Agentic Coding Workflow.

Stage 0 establishes the trustworthy starting context for a project before service goal definition, requirements, domain modeling, architecture, data design, task breakdown, or implementation begins.

---

## 1. What This Skill Is For

Use this skill to determine:

- whether the project is greenfield, brownfield, prototype, research tool, migration, maintenance, or extension work;
- what project profile applies, such as MVP production, internal tool, mobile app, AI/data product, web SaaS, or regulated/security-sensitive system;
- what the human developer has already decided;
- what is still only a working assumption;
- what is unknown or needs human clarification;
- what documents, code, tests, data, infrastructure, or deployment settings already exist;
- what technology stack or platform choices are fixed;
- what areas must not be changed;
- what early security, privacy, data, operational, or research risks are visible;
- whether the next step should be Stage 1 Service Goal Definition or a deeper existing-codebase review.

The goal of this stage is not to design or implement the system. The goal is to prevent later stages from relying on vague, missing, stale, or unapproved context.

---

## 2. Files in This Skill Folder

Recommended folder structure:

```text
/skills/00_project_intake/
  README.md
  SKILL.md
  artifact_contract.yml
  validation_checklist.md        # optional
  example_inputs.md              # optional
  example_outputs.md             # optional
```

File roles:

| File | Main reader | Role |
|---|---|---|
| `README.md` | Human developer / workflow maintainer | User guide for when and how to run this skill |
| `SKILL.md` | Agent | Executable reusable procedure for Stage 0 |
| `artifact_contract.yml` | Agent / tooling / human developer | Official artifact contract for Stage 0 outputs and handoff expectations |
| `validation_checklist.md` | Human developer / agent | Optional review checklist |
| `example_inputs.md` | Human developer / agent | Optional examples of valid intake inputs |
| `example_outputs.md` | Human developer / agent | Optional examples of expected Stage 0 outputs |

`README.md` should not duplicate the full execution procedure in `SKILL.md`. It should help the human developer understand how to use the skill.

---

## 3. When to Use This Skill

Use this skill when:

- starting a new Manual Agentic Coding Workflow;
- receiving a new project idea;
- entering a repository or project folder for the first time;
- deciding whether work is greenfield, brownfield, prototype, research, migration, maintenance, or extension work;
- initializing `/workflow` and `/workflow/context` files;
- preparing the handoff to Stage 1 Service Goal Definition;
- deciding whether a deeper codebase-context-review skill should run before Stage 1.

Do not use this skill to:

- define final service goals;
- decompose requirements;
- write acceptance criteria;
- perform domain modeling;
- design architecture, APIs, data schemas, or infrastructure;
- create task breakdowns;
- write implementation prompts;
- edit production code.

---

## 4. What the User Should Prepare Before Running

Stage 0 can run with very little information, but better inputs produce better intake results.

At minimum, provide one of the following:

```text
- a short project idea or problem statement; or
- a repository/project folder to inspect; or
- a stage-local USER_DIRECTIVES.md file describing what is already known.
```

Recommended user-provided information:

```text
- initial project idea
- target users or stakeholders, if known
- whether this is a new project or existing system
- fixed technology choices, if any
- forbidden technologies or forbidden change areas
- existing documents or repository locations
- existing deployment or infrastructure context
- existing data, datasets, or database context
- security, privacy, legal, or compliance concerns
- preferred project profile, if already known
- questions the agent must answer during intake
```

For a project-specific run, place additional instructions here:

```text
/workflow/00_intake/USER_DIRECTIVES.md
```

Example:

```markdown
# USER_DIRECTIVES.md

## Project Summary
Build a web-based evaluation tool for expert review of LLM-generated analysis results.

## Explicit Decisions
- Frontend: Flutter
- Backend: Firebase
- Database: Firestore

## Preferences
- Keep MVP scope small.
- Avoid unnecessary enterprise architecture.

## Questions for Stage 0
- Should this be treated as a research tool, MVP production project, or both?
- Is deeper codebase review needed before Stage 1?
```

---

## 5. Are Skill Inputs Recorded in `artifact_contract.yml`?

Usually, the detailed input contract belongs in `SKILL.md`, not primarily in `artifact_contract.yml`.

Use the files this way:

| File | Should contain input information? | Recommended role |
|---|---:|---|
| `README.md` | Yes, as user-facing guidance | Explain what the human should prepare before running the skill |
| `SKILL.md` | Yes, as the authoritative execution contract | Define Always Check, Read If Applicable, Do Not Read By Default, and Missing Input Handling |
| `artifact_contract.yml` | Optionally, as a concise machine-readable summary | Define official outputs, conditional outputs, N/A rules, and next-stage handoff; optionally list expected runtime inputs |
| `/workflow/context/artifact_manifest.yml` | No, not as a design-time input contract | Record actual artifact existence, status, approval, and supersession during a project |
| `/workflow/context/context_packet.md` | Yes, for next-stage handoff | Record the minimal inputs the next stage should read |

Recommended rule:

```text
README.md tells the human what to prepare.
SKILL.md tells the agent what to read and how to handle missing inputs.
artifact_contract.yml tells the workflow what outputs and handoff artifacts this stage must produce.
```

It is acceptable to include a small `runtime_inputs` or `expected_inputs` section in `artifact_contract.yml`, but it should be a summary only. Do not make `artifact_contract.yml` replace the input contract in `SKILL.md`.

If you want strict machine-readable input validation later, create a separate `input_contract.yml` or add a small `input_contract` section to `artifact_contract.yml`.

---

## 6. Typical Runtime Input Locations

During execution, the agent should check these files if they exist:

```text
/workflow/00_intake/USER_DIRECTIVES.md
/workflow/00_intake/review_notes.md
/workflow/context/artifact_manifest.yml
/workflow/context/context_packet.md
/workflow/context/DECISIONS.md
/workflow/context/ASSUMPTIONS.md
/workflow/context/OPEN_QUESTIONS.md
/workflow/context/REJECTED_OPTIONS.md
/workflow/context/TRACEABILITY_MATRIX.md
/workflow/context/APPROVAL_LOG.md
```

For the first Stage 0 run, many of these files may not exist yet. That is expected. The agent should initialize or propose them as appropriate instead of treating their absence as an automatic failure.

Conditional repository or project files may include:

```text
README.md
/docs/
/product/
/specs/
package.json
pyproject.toml
requirements.txt
pubspec.yaml
firebase.json
firestore.rules
Dockerfile
vercel.json
/tests/
/.github/workflows/
```

The agent should not read the entire source tree by default. It should read only files relevant to intake.

---

## 7. Runtime Output Locations

Stage execution results are written to the project execution layer, not to the reusable skill folder.

Expected output locations:

```text
/workflow/00_intake/00_project_intake.md
/workflow/00_intake/00_existing_context_review.md   # conditional
/workflow/00_intake/result.md
/workflow/context/context_packet.md
/workflow/context/artifact_manifest.yml             # if initialized or updated
/workflow/context/ASSUMPTIONS.md                    # if assumptions are recorded
/workflow/context/OPEN_QUESTIONS.md                 # if open questions are recorded
/workflow/context/REJECTED_OPTIONS.md               # if rejected options are recorded
/workflow/context/TRACEABILITY_MATRIX.md            # if initialized or updated
/workflow/context/APPROVAL_LOG.md                   # only if explicit approval is provided
```

---

## 8. Typical Execution Command

Use a command like this in an agentic coding tool:

```text
Read and execute /skills/00_project_intake/SKILL.md.

Use /workflow/00_intake/USER_DIRECTIVES.md if it exists.
Check existing /workflow/context files if they exist.
Create or update the required Stage 0 artifacts under /workflow/00_intake and /workflow/context.
Do not start requirements, architecture, data design, task breakdown, or implementation.
End with the human approval gate.
```

For a first run with only an idea:

```text
Read /skills/00_project_intake/SKILL.md and execute Stage 0 Project Intake.

Initial project idea:
[[PASTE PROJECT IDEA HERE]]

Create the Stage 0 intake artifacts and prepare context_packet.md for the next stage.
Do not proceed to Stage 1 until approval items are listed.
```

For an existing repository:

```text
Read /skills/00_project_intake/SKILL.md and execute Stage 0 Project Intake for this repository.

Inspect only high-level project context first: README, docs, package/config files, test/deployment indicators, and workflow context files if present.
Do not read the full source tree by default.
Determine whether a deeper codebase-context-review skill is needed before Stage 1.
```

---

## 9. Human Approval Required

Stage 0 should end with approval requests for:

```text
- project context type
- project profile
- greenfield / brownfield / prototype / research / migration / extension / maintenance classification
- fixed technology stack, if any
- source documents, code, tests, data, or deployment context to trust
- forbidden change areas
- initial security, privacy, data, and operational constraints
- whether deeper codebase-context-review is needed
- next recommended stage
```

Do not treat agent classification as approved unless the human explicitly approves it.

---

## 10. Completion Criteria

Stage 0 is complete when:

```text
[ ] /workflow/00_intake/00_project_intake.md exists.
[ ] /workflow/00_intake/result.md exists.
[ ] /workflow/context/context_packet.md exists or is updated.
[ ] /workflow/00_intake/00_existing_context_review.md is created or explicitly marked N/A.
[ ] Project type and profile are identified as approved, candidate, or uncertain.
[ ] Approved decisions, assumptions, open questions, risks, and rejected options are separated.
[ ] Early security/privacy/data/LLM/API/operational risk signals are recorded if visible.
[ ] The next recommended step is clearly stated.
[ ] Human approval items are clearly listed.
```

---

## 11. Recommended Next Step After Stage 0

After Stage 0, the usual next step is:

```text
Stage 1 Service Goal Definition
```

However, run a deeper codebase-context-review first if Stage 0 finds:

```text
- existing production system
- existing codebase with compatibility constraints
- migration or modernization context
- deployment/infrastructure that must be preserved
- production data or existing database
- fragile modules or forbidden change areas
- existing tests/CI that must be respected
```

---

## 12. Maintenance Notes

Keep this README short and user-facing.

Do not copy the full `SKILL.md` execution procedure into this README. If the execution rules change, update `SKILL.md` first and then revise this README only where the user-facing guidance changes.

If the official artifact set changes, update `artifact_contract.yml` and ensure `SKILL.md` reflects the same output responsibilities.
