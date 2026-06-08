# Concept: Manual Agentic Coding Workflow

This document explains the design concept behind the Manual Agentic Coding Workflow.

For a short usage path, start with [`QUICKSTART.md`](./QUICKSTART.md). For the stage-by-stage process, see [`WORKFLOW_OVERVIEW.md`](./WORKFLOW_OVERVIEW.md).

## 1. Core idea

This workflow is based on a simple premise:

```text
Agentic Coding = structured workflow + reusable skills + explicit artifacts + human approval gates + traceable context handoff
```

It is not designed to let an AI agent autonomously build a system from a vague request. It is designed to help an experienced human developer use coding agents inside a controlled, inspectable, and repeatable software development process.

The workflow transforms software development from this:

```text
vague request
→ direct code generation
→ manual cleanup
```

into this:

```text
structured context
→ approved goals
→ verifiable requirements
→ domain model
→ architecture and data contracts
→ scoped tasks
→ implementation prompts
→ TDD implementation
→ review and release
→ workflow improvement
```

The agent does not own the software process. The human developer owns the process. The agent executes structured work inside that process.

## 2. Why this workflow exists

Coding agents can be useful, but unmanaged agentic coding often fails in predictable ways:

- requirements are vague or silently invented;
- agent assumptions become accidental design decisions;
- scope expands without approval;
- design and implementation drift apart;
- previous decisions are forgotten after context resets;
- tests are added too late or not at all;
- security and privacy are reviewed too late;
- implementation evidence is weak;
- handoff documentation is incomplete;
- rejected ideas reappear in later sessions.

The workflow addresses these problems by forcing each stage to produce concrete artifacts and by requiring human approval before those artifacts become downstream source of truth.

## 3. What this workflow is

Manual Agentic Coding Workflow is:

- an artifact-first SDLC workflow for coding agents;
- a reusable stage structure for planning, designing, implementing, testing, reviewing, and improving software projects;
- a way to preserve project context across agent sessions using files instead of chat history;
- a method for separating approved decisions from assumptions, recommendations, and open questions;
- a practical structure for integrating TDD, DDD, security, privacy, review, release, and retrospective work;
- a learning environment for studying how agents reason, fail, recover, and improve.

## 4. What this workflow is not

This workflow is not:

- an autonomous software engineer;
- a one-shot app generator;
- a replacement for experienced engineering judgment;
- a collection of disconnected prompts;
- a guarantee that generated code is correct, secure, or production-ready;
- a process where agent output automatically becomes an approved project decision.

The workflow is intentionally manual. The human developer reviews, modifies, approves, rejects, or redirects the agent's work.

## 5. Fundamental distinctions

The workflow depends on these distinctions:

```text
Agent proposal ≠ approved decision
Agent inference ≠ verified fact
Agent assumption ≠ requirement
Agent draft ≠ final artifact
Agent output ≠ human approval
```

These distinctions prevent the agent from silently converting guesses into project truth.

### Approved decision

A decision explicitly approved by the human developer.

Example:

```text
Approved: The MVP will use Firebase Authentication.
```

### Decision candidate

A recommendation that still requires human approval.

Example:

```text
Candidate: Use role-based access control with Admin, Reviewer, and Viewer roles.
```

### Working assumption

A temporary belief used to make progress, not yet verified.

Example:

```text
Assumption: The first release targets a web MVP rather than a mobile app.
```

### Open question

An unresolved issue that may affect later requirements, design, implementation, validation, or release.

Example:

```text
Open Question: Should reviewers be able to revise submitted evaluations?
```

### Rejected option

An option that should not be revived unless the human explicitly reopens it.

Example:

```text
Rejected: Do not use a relational database for the MVP unless the data model changes.
```

## 6. Human and agent roles

### Human developer

The human developer:

- owns the process;
- supplies project intent and constraints;
- reviews generated artifacts;
- approves or rejects decisions;
- resolves conflicts and trade-offs;
- decides when to move to the next stage;
- decides when the workflow itself should be changed.

### Agent

The agent:

- reads approved context;
- follows the current `SKILL.md`;
- reads only the necessary inputs;
- checks stage-local `USER_DIRECTIVES.md` when present;
- creates or updates required artifacts;
- identifies missing information and uncertainty;
- separates decisions, assumptions, open questions, risks, and recommendations;
- prepares the next stage's context;
- reports what requires human approval.

The agent should be treated as a structured development assistant, not as an autonomous developer.

## 7. SKILL.md is not just a prompt

In this workflow, a `SKILL.md` is a reusable procedure document.

A skill defines:

- when to use it;
- which stage it belongs to;
- what inputs the agent must read;
- which inputs are conditional;
- what must not be read by default;
- how to handle missing or conflicting information;
- which artifacts to create or update;
- how to update `context_packet.md`;
- how to preserve traceability;
- what requires human approval;
- what the agent must not do.

A skill is therefore closer to an operating procedure than a one-time prompt.

Project-specific information should come from artifacts, `context_packet.md`, `artifact_manifest.yml`, `USER_DIRECTIVES.md`, project profiles, and specialization addenda — not from rewriting the skill every time.

## 8. Artifact-first workflow

The workflow uses files as the durable project memory.

Typical artifacts include:

```text
/workflow/01_goal/01_service_goal.md
/workflow/03_requirements/03_requirements.md
/workflow/03_requirements/03_acceptance_criteria.md
/workflow/04_domain/04_domain_model.md
/workflow/05_architecture/05_architecture_plan.md
/workflow/06_data/06_logical_schema.md
/workflow/08_test_strategy/08_test_strategy.md
/workflow/09_tasks/09_task_cards.md
/workflow/10_prompts/10_implementation_prompts.md
/workflow/11_implementation_results/11_test_evidence_<task_id>.md
/workflow/12_review_release_handoff/12_release_readiness.md
```

Chat history can help within a single session, but it should not be the source of truth for later stages.

Downstream stages should rely on approved artifacts, not on memory of previous conversations.

## 9. Context management

The workflow uses persistent context files to make agent sessions restartable.

Recommended context files:

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

### context_packet.md

`context_packet.md` is not a full project history. It is the minimum operational context required by the next stage.

It should include:

- current project state;
- approved decisions relevant to the next stage;
- active working assumptions;
- open questions that may affect later work;
- rejected or superseded options;
- constraints that must not be violated;
- key context for the next stage;
- required inputs for the next stage;
- things the next agent must not do.

Use `context_packet.md` as a navigation layer, not as the only source of truth. Important details should remain in the original artifacts.

### DECISIONS.md

Stores only human-approved decisions.

### ASSUMPTIONS.md

Stores useful but unverified working assumptions.

### OPEN_QUESTIONS.md

Stores unresolved issues that may affect later workflow stages.

### REJECTED_OPTIONS.md

Stores rejected or superseded options so the agent does not revive them later.

### TRACEABILITY_MATRIX.md

Maintains links such as:

```text
Goal
→ Requirement
→ Acceptance Criteria
→ Domain Concept
→ Architecture Component
→ Data Model
→ Task
→ Test
→ Implementation Evidence
```

## 10. Human approval gates

Every major stage should end with a human approval gate.

The approval gate should identify:

- decisions to approve;
- assumptions to confirm;
- open questions to resolve;
- risks to review;
- artifacts ready for review;
- recommended next step.

The agent must not claim that an artifact is approved unless the human explicitly approves it.

Human approval is especially important for:

- service goal;
- MVP scope;
- non-goals;
- roles and permissions;
- personal data handling;
- external API or LLM data transfer;
- domain terminology;
- aggregate and bounded context decisions;
- architecture direction;
- database schema;
- API contracts;
- release order;
- implementation prompts;
- deployment;
- workflow improvement priorities.

## 11. Traceability as a control mechanism

Traceability is not documentation overhead. It is a control mechanism for agent work.

Traceability helps answer:

- Why does this task exist?
- Which requirement does this test validate?
- Which domain rule does this code enforce?
- Which architecture decision does this file implement?
- What evidence proves the task is complete?

A useful traceability chain looks like this:

```text
Goal
→ Requirement
→ Acceptance Criteria
→ Domain Rule
→ Architecture / Data Contract
→ Task Card
→ Implementation Prompt
→ Test Evidence
→ Review Result
```

If a task cannot be linked to a requirement or approved goal, it may be scope creep.

If a requirement cannot be linked to validation, it may not be testable enough.

## 12. TDD integration

TDD is not treated as a final testing step. It appears throughout the workflow.

### Requirements stage

Requirements must be connected to acceptance criteria.

```text
Requirement → Acceptance Criteria
```

### Test strategy stage

Acceptance criteria are translated into validation methods.

```text
Acceptance Criteria → Test Case / Manual Verification / Validation Command
```

### Task breakdown stage

Each task specifies required tests and definition of done.

```text
Task → Required Tests → Evidence
```

### Implementation stage

Implementation uses a test-first or test-aware loop.

```text
identify or write failing test
→ confirm failure if feasible
→ implement minimal change
→ pass relevant tests
→ refactor
→ run broader validation
→ record evidence
```

If strict test-first development is not feasible, the agent must explain why and create a test-aware validation plan before implementation.

## 13. DDD integration

DDD is centered in Stage 04 but influences architecture, data design, tasks, and tests.

In this workflow, DDD means:

- ubiquitous language;
- domain concepts;
- entities;
- value objects;
- aggregates;
- invariants;
- lifecycle and state transitions;
- domain events;
- bounded contexts;
- context maps.

It does not mean designing database tables first.

Important mappings:

```text
Invariant → Unit Test
State Transition → Scenario Test
Domain Event → Integration Test
Bounded Context → Module Boundary
Aggregate → Transaction Boundary
```

DDD helps preserve business meaning through implementation and validation.

## 14. Security and privacy integration

Security and privacy are considered throughout the workflow, not only at release time.

Typical integration points:

```text
Stage 02: early risk and privacy screening
Stage 03: security and privacy requirements
Stage 05: authentication, authorization, data flow, integration boundaries
Stage 06: data access rules, retention, deletion, indexes, migration risks
Stage 08: validation of security-sensitive behavior
Stage 11: task-level security notes and validation evidence
Stage 12: final security and privacy review
```

The agent should identify:

- personal data;
- sensitive data;
- role-based access needs;
- administrator powers;
- external API or LLM data transfer;
- audit logging needs;
- retention and deletion needs;
- security assumptions;
- privacy risks;
- release blockers.

## 15. Stage facade pattern for large stages

Some stages are too large to execute reliably as one skill. In that case, the stage can be split internally into sub-skills.

The important rule is:

```text
Split work internally.
Expose one stage package externally.
Preserve official artifacts.
Require finalizer consolidation.
Make downstream stages depend only on approved artifacts.
```

For example, Stage 04 Domain Modeling may be split internally:

```text
04_domain_modeling
  → 04a_ubiquitous_language
  → 04b_domain_concepts_entities_values
  → 04c_aggregates_rules_lifecycle
  → 04d_events_bounded_contexts
  → 04e_domain_modeling_finalizer
```

But downstream Stage 05 Architecture should depend only on approved official Stage 04 artifacts, not on internal sub-skill folders or prompt history.

## 16. Project profiles and specialization

The same workflow can be adapted to different project types.

Common profiles:

```text
Prototype / Research Tool
MVP Production
Regulated / Security-Sensitive
```

Common specialization addenda:

```text
web_saas
internal_tool
mobile_app
ai_data_product
regulated_security_sensitive
brownfield_legacy
```

Specialization addenda may add inputs, questions, artifacts, validation needs, and approval requirements.

They should not replace the stage-specific skill or weaken the core approval and artifact rules.

## 17. Context reset tolerance

The workflow is designed so that a new agent session can start from files only.

This is important because agent tools may have context limits, chat sessions may be cleared, and different tools may be used at different stages.

A new session should be able to continue by reading:

```text
1. The current SKILL.md
2. artifact_manifest.yml
3. context_packet.md
4. DECISIONS.md
5. relevant approved source artifacts
6. USER_DIRECTIVES.md if present
```

The workflow should not depend on invisible chat memory.

## 18. Common anti-patterns

Avoid these patterns:

- asking the agent to build the product directly from a vague idea;
- treating generated output as approved by default;
- recording agent recommendations in `DECISIONS.md` without human approval;
- using `context_packet.md` as the only source of truth;
- reading all historical files by default;
- ignoring `USER_DIRECTIVES.md`;
- reviving rejected options;
- changing official artifact paths because internal skill paths changed;
- making downstream stages depend on sub-skill internals;
- skipping validation evidence;
- claiming tests passed without running or recording evidence;
- doing security and privacy review only at the end;
- letting implementation tasks drift away from requirements and acceptance criteria.

## 19. When to simplify the workflow

The full workflow is useful for serious MVPs, internal systems, production-facing tools, or projects where learning agent behavior is part of the goal.

For small prototypes, you may simplify by:

- using lighter artifacts;
- merging some early planning stages;
- reducing approval gates;
- keeping manual validation instead of full automated test coverage;
- running fewer sub-skills;
- documenting assumptions more briefly.

Even in simplified mode, preserve these rules:

```text
Do not silently convert assumptions into decisions.
Do not implement before requirements are testable enough.
Do not skip validation evidence.
Do not depend on chat history as source of truth.
```

## 20. Recommended reading order

For new users:

```text
README.md
→ QUICKSTART.md
→ CONCEPT.md
→ WORKFLOW_OVERVIEW.md
```

For people designing or modifying skills:

```text
CONCEPT.md
→ WORKFLOW_OVERVIEW.md
→ workflow_templates/core/core_skill_template.md
→ workflow_templates/stages/*
→ skills/*/SKILL.md
```

For people executing a real project:

```text
QUICKSTART.md
→ Stage 00 SKILL.md
→ Stage 00 outputs
→ Stage 01 SKILL.md
→ continue stage by stage
```
