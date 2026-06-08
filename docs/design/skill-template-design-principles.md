# SKILL Template Design Principles for Manual Agentic Coding Workflow

> 이 문서는 Manual Agentic Coding Workflow에서 모든 stage/step의 `SKILL.md`를 설계할 때 사용할 원칙과 절차를 정리한 문서이다.  
> LLM 또는 coding agent에게 전달하여 reusable skill template, stage-specific skill, project-type specialization, tool wrapper를 설계할 때 기준 문서로 사용한다.

---

## 1. Purpose

이 문서의 목적은 다음을 명확히 하는 것이다.

1. 모든 SKILL을 하나의 공통 구조로 표준화할 수 있는가?
2. 시스템 유형별로 별도 common template을 만들지 않고, 작은 core template을 specialization하는 방식이 적절한가?
3. stage별 산출물과 이전 stage 입력 파일을 미리 정의할 수 있는가?
4. 각 stage에서 어떤 이전 산출물을 읽을지 언제, 어떻게 결정해야 하는가?
5. LLM/Agent가 SKILL을 실행할 때 매번 prompt를 수정하지 않고도 안정적으로 작업하도록 만들 수 있는가?

핵심 결론은 다음과 같다.

```text
SKILL은 매번 수정하는 일회용 prompt가 아니다.
SKILL은 재사용 가능한 절차 문서이다.
프로젝트별 차이는 artifact, context_packet, USER_DIRECTIVES, project profile, specialization addendum이 처리한다.
```

---

## 2. Core Design Premise

Manual Agentic Coding Workflow의 기본 premise는 다음과 같다.

```text
Agentic Coding = structured workflow + reusable skills + explicit artifacts + human approval gates + traceable context handoff
```

Agent는 자율 개발자가 아니다. Agent는 다음 역할을 수행한다.

```text
1. 승인된 context를 읽는다.
2. 현재 stage의 목적을 이해한다.
3. 필요한 이전 산출물만 읽는다.
4. stage-local user directive를 반영한다.
5. 현재 stage의 산출물을 만든다.
6. 사실, 가정, 제안, 승인된 결정, open question을 분리한다.
7. 다음 stage가 필요한 최소 context를 준비한다.
8. human approval이 필요한 항목을 명시한다.
```

반드시 유지해야 하는 원칙은 다음과 같다.

```text
Agent proposal ≠ Approved decision
Agent inference ≠ Verified fact
Agent assumption ≠ Requirement
Agent candidate design ≠ Final design
Agent output ≠ Approved artifact
```

---

## 3. Recommended Template Architecture

시스템 유형별로 완전히 다른 common template을 여러 개 만들지 않는다. 대신 다음 계층 구조를 사용한다.

```text
Core Skill Template
→ Stage-Specific Skill Template
→ Project-Type Specialization Addendum
→ Tool-Specific Wrapper
```

### 3.1 Core Skill Template

모든 SKILL이 반드시 따르는 최소 공통 규칙이다.

포함해야 하는 항목:

```text
- Agent role and operating mode
- approved decision / assumption / open question 구분 규칙
- USER_DIRECTIVES.md 확인 규칙
- input precedence rules
- required output artifact rules
- context_packet.md update rules
- human approval gate
- anti-patterns / do-not-do rules
```

포함하지 않는 것이 좋은 항목:

```text
- requirements 작성법의 세부 내용
- DDD aggregate 설계법
- API contract 세부 설계법
- database schema 설계법
- TDD implementation loop의 세부 절차
- security review checklist 전체
```

이런 내용은 stage-specific skill 또는 addendum으로 분리한다.

---

### 3.2 Stage-Specific Skill Template

각 stage가 고유하게 수행해야 하는 작업, 입력, 산출물, 검증 기준을 정의한다.

예시:

```text
Stage 3 Requirements & Acceptance Criteria
- service goal을 requirements로 분해한다.
- functional / non-functional requirement를 구분한다.
- acceptance criteria를 작성한다.
- testability를 점검한다.

Stage 4 Domain Modeling / DDD
- ubiquitous language를 정의한다.
- entities, value objects, aggregates, invariants를 식별한다.
- domain events와 bounded contexts를 정리한다.

Stage 8 Test Strategy & Validation Harness
- unit/integration/E2E/manual validation 전략을 정의한다.
- requirement별 validation method를 연결한다.
- test commands와 pass/fail criteria를 정리한다.
```

Stage-specific template은 다음을 반드시 정의해야 한다.

```text
- Purpose
- Core question
- Always Read inputs
- Read If Applicable inputs
- Do Not Read By Default inputs
- Output artifact contract
- Traceability requirements
- Stage-specific acceptance criteria
- Stage-specific human approval gate
- Next context_packet.md update rules
```

---

### 3.3 Project-Type Specialization Addendum

시스템 유형별 차이는 별도 common template이 아니라 addendum으로 처리한다.

권장 project-type addendum:

```text
- web_saas.md
- internal_tool.md
- mobile_app.md
- ai_data_product.md
- regulated_security_sensitive.md
- brownfield_legacy.md
```

Specialization addendum은 다음을 추가한다.

```text
- additional inputs
- additional questions
- additional artifacts
- additional validation needs
- additional risks
- additional approval requirements
```

예시: `ai_data_product.md`

```markdown
# AI/Data Product Specialization

## Additional Inputs
- dataset description
- data provenance
- labeling policy
- evaluation metrics
- model risk assumptions

## Additional Requirements Questions
- What data is used?
- What labels are trusted?
- What evaluation metric defines success?
- What failure modes are unacceptable?
- Is human review required?

## Additional Validation Needs
- dataset split validation
- benchmark evaluation
- bias/error analysis
- reproducibility record
- model output review
```

Specialization은 stage-specific skill을 대체하지 않는다. 필요한 경우 stage-specific skill에 추가로 적용된다.

---

### 3.4 Tool-Specific Wrapper

Claude Code, Codex, Antigravity 등 도구별 차이는 별도 wrapper에서 처리한다.

Tool wrapper는 다음만 다룬다.

```text
- skill file location
- tool-specific metadata
- command invocation convention
- artifact output location
- sandbox / permission / hook 관련 실행 규칙
- review UI 또는 artifact review 방식
```

Tool wrapper는 domain, requirement, architecture 등의 설계 판단 내용을 포함하지 않는다.

---

## 4. Recommended Repository Structure

```text
/workflow_templates
  /core
    core_skill_template.md
    context_rules.md
    approval_rules.md
    artifact_rules.md

  /stages
    00_project_intake_skill_template.md
    01_service_goal_skill_template.md
    02_stakeholder_risk_skill_template.md
    03_requirements_skill_template.md
    04_domain_modeling_skill_template.md
    05_architecture_skill_template.md
    06_data_design_skill_template.md
    07_mvp_release_skill_template.md
    08_test_strategy_skill_template.md
    09_task_breakdown_skill_template.md
    10_implementation_prompt_skill_template.md
    11_implementation_loop_skill_template.md
    12_review_release_skill_template.md
    13_retrospective_skill_template.md

  /specializations
    web_saas.md
    internal_tool.md
    mobile_app.md
    ai_data_product.md
    regulated_security_sensitive.md
    brownfield_legacy.md

  /tool_wrappers
    claude_code_wrapper.md
    codex_wrapper.md
    antigravity_wrapper.md
```

실제 프로젝트에는 다음 구조를 사용한다.

```text
/workflow
  /00_intake
  /01_goal
  /02_stakeholders_risk
  /03_requirements
  /04_domain
  /05_architecture
  /06_data
  /07_mvp_release
  /08_test_strategy
  /09_tasks
  /10_prompts
  /11_implementation_results
  /12_review_release_handoff
  /13_retrospective

/workflow/context
  artifact_manifest.yml
  context_packet.md
  DECISIONS.md
  ASSUMPTIONS.md
  OPEN_QUESTIONS.md
  REJECTED_OPTIONS.md
  TRACEABILITY_MATRIX.md
  APPROVAL_LOG.md
```

---

## 5. Stage Artifact Contract

Stage별 산출물은 미리 정의할 수 있다. 그러나 모든 시스템에 대해 완전히 고정된 파일 목록을 강제하지 않는다.

권장 방식은 `Stage Artifact Contract`이다.

```text
Stage Artifact Contract = Mandatory Artifacts + Conditional Artifacts + N/A Record + Next Context Rules
```

### 5.1 Mandatory Artifacts

모든 프로젝트에서 해당 stage가 반드시 생성해야 하는 core artifact이다.

예시:

```text
Stage 1 Goal
- 01_service_goal.md

Stage 3 Requirements
- 03_requirements.md
- 03_acceptance_criteria.md

Stage 8 Test Strategy
- 08_test_strategy.md
- 08_validation_commands.md
```

### 5.2 Conditional Artifacts

시스템 특성에 따라 생성하는 artifact이다.

예시:

```text
Stage 5 Architecture
- 05_api_contracts.md, if APIs exist
- 05_integration_contracts.md, if external systems exist
- 05_authz_model.md, if roles or permissions exist
- 05_event_contracts.md, if async messaging exists

Stage 6 Data Design
- 06_logical_schema.md, if persistent data exists
- 06_indexes.md, if query optimization is needed
- 06_data_security_rules.md, if access control is data-dependent
- 06_migration_plan.md, if schema/data migration is needed
```

### 5.3 N/A Record

적용되지 않는 산출물은 조용히 생략하지 않는다. 왜 필요 없는지 기록한다.

예시:

```text
No persistent data is used in this project.
Therefore, physical schema, indexes, and migration plan are not applicable.
This decision should be revisited if the project later introduces persistent user data.
```

---

## 6. Input Contract for Each SKILL

각 SKILL은 이전 산출물 중 무엇을 읽을지 미리 정의해야 한다.

```text
Input Contract = Always Read + Read If Applicable + Do Not Read By Default + Missing Input Handling
```

### 6.1 Always Read

현재 stage를 실행할 때 항상 필요한 입력이다.

예시: Stage 8 Test Strategy

```text
Always Read:
- /workflow/context/context_packet.md
- /workflow/context/DECISIONS.md
- /workflow/03_requirements/03_requirements.md
- /workflow/03_requirements/03_acceptance_criteria.md
- /workflow/05_architecture/05_architecture_plan.md
- /workflow/07_mvp_release/07_mvp_scope.md
```

### 6.2 Read If Applicable

project profile, context_packet, USER_DIRECTIVES, DECISIONS를 보고 조건이 충족될 때만 읽는다.

예시:

```text
Read If Applicable:
- /workflow/04_domain/04_business_rules_invariants.md
  if domain invariants exist

- /workflow/05_architecture/05_api_contracts.md
  if the system exposes APIs

- /workflow/06_data/06_data_security_rules.md
  if database access rules exist

- /workflow/00_intake/00_existing_context_review.md
  if this is a brownfield project
```

### 6.3 Do Not Read By Default

필요하지 않으면 읽지 않는 입력이다.

```text
Do Not Read By Default:
- full historical result files from unrelated stages
- raw agent logs
- superseded artifacts
- rejected artifacts
- draft artifacts not needed for the current stage
```

### 6.4 Missing Input Handling

필수 입력이 없거나 승인되지 않았을 때의 처리 규칙이다.

```text
If a required input is missing:
1. Report it under Missing Information.
2. Explain why it matters.
3. Decide whether it is blocking.
4. If progress is possible, continue with a clearly labeled working assumption.
5. If progress is unsafe, stop and request human decision.
```

---

## 7. When and How Input Selection Is Decided

이전 산출물 중 무엇을 사용할지는 한 번에 결정하지 않는다. 세 시점에서 결정한다.

```text
1. Workflow design time
2. Project intake / profile selection time
3. Stage execution preflight time
```

### 7.1 Workflow Design Time

Workflow 또는 SKILL template 설계자가 stage별 표준 input contract를 정의한다.

예시:

```text
Stage 5 Architecture Always Read:
- service goal
- stakeholders and risks
- requirements
- acceptance criteria
- domain model
- approved decisions
```

이 단계에서는 시스템 유형과 무관하게 stage가 원칙적으로 필요로 하는 입력을 정의한다.

---

### 7.2 Project Intake / Profile Selection Time

Stage 0에서 프로젝트 유형을 결정한다.

예시:

```text
- greenfield
- brownfield
- prototype
- MVP production
- research tool
- web SaaS
- mobile app
- AI/data product
- regulated/security-sensitive system
```

Project profile은 conditional input을 활성화하거나 비활성화한다.

예시:

```text
web_saas → API contract, auth model, data security rules 활성화
mobile_app → device permission, offline/sync, app release notes 활성화
ai_data_product → dataset design, evaluation metrics, model risk notes 활성화
brownfield → codebase review, regression baseline, compatibility constraints 활성화
regulated → threat model, audit log policy, privacy impact notes 활성화
```

---

### 7.3 Stage Execution Preflight Time

각 stage 실행 직전에 Agent가 실제 읽기 목록을 최종 확인한다.

Preflight checklist:

```text
[ ] artifact_manifest.yml을 읽었다.
[ ] context_packet.md의 Required Inputs for Next Stage를 확인했다.
[ ] SKILL.md의 Always Read 목록을 확인했다.
[ ] project profile에 따른 conditional inputs를 확인했다.
[ ] USER_DIRECTIVES.md가 추가 입력을 요구하는지 확인했다.
[ ] required artifact가 존재하는지 확인했다.
[ ] required artifact가 approved 상태인지 확인했다.
[ ] superseded/rejected artifact를 사용하지 않았는지 확인했다.
[ ] conflict가 있으면 보고했다.
```

---

## 8. Role of Key Context Files

### 8.1 `SKILL.md`

`SKILL.md`는 재사용 가능한 절차 문서이다.

```text
SKILL.md는 매번 수정하지 않는다.
SKILL.md는 어떤 종류의 산출물을 읽어야 하는지 미리 안다.
SKILL.md는 현재 프로젝트의 실제 내용은 artifact를 읽고 파악한다.
```

`SKILL.md`가 포함해야 하는 것:

```text
- skill purpose
- stage and step
- input contract
- execution procedure
- output artifact contract
- context update rule
- validation checklist
- human approval gate
```

---

### 8.2 `context_packet.md`

`context_packet.md`는 전체 프로젝트 history가 아니다. 다음 stage가 필요한 최소 operational context이다.

중요 원칙:

```text
context_packet.md is a navigation layer, not the sole source of truth.
```

`context_packet.md`는 다음을 포함한다.

```text
- current project state
- approved decisions summary
- active assumptions
- open questions affecting next steps
- rejected or superseded options
- constraints that must not be violated
- key context for the next stage
- required inputs for the next stage
- do-not-do instructions
```

단, 중요한 결정은 원본 artifact, DECISIONS.md, APPROVAL_LOG.md로 확인해야 한다.

---

### 8.3 `artifact_manifest.yml`

`artifact_manifest.yml`은 artifact의 존재, 상태, 승인 여부, superseded 여부를 관리한다.

예시:

```yaml
artifacts:
  - id: 03_requirements_v1
    path: /workflow/03_requirements/03_requirements.md
    stage: 03_requirements
    status: approved
    approved_by: human
    approved_at: 2026-06-07
    supersedes: null
    source_artifacts:
      - /workflow/01_goal/01_service_goal.md
      - /workflow/02_stakeholders_risk/02_stakeholders.md
```

Agent는 stage 실행 전 manifest를 확인해야 한다.

```text
Only approved artifacts may be used as source of truth unless exploratory work is explicitly requested.
```

---

### 8.4 `USER_DIRECTIVES.md`

`USER_DIRECTIVES.md`는 stage-local human instruction file이다.

포함할 수 있는 내용:

```text
- user requirements
- user preferences
- explicit approvals
- rejections
- corrections to previous Agent output
- scope changes
- review comments
- additional constraints
- questions the Agent must answer
```

처리 원칙:

```text
- USER_DIRECTIVES.md가 있으면 stage 실행 전에 반드시 읽는다.
- user directive를 agent assumption보다 우선한다.
- directive가 approved decision인지 단순 preference인지 구분한다.
- approved decision과 충돌하면 조용히 덮어쓰지 말고 conflict로 보고한다.
- USER_DIRECTIVES.md를 자동으로 수정하지 않는다.
```

---

### 8.5 `DECISIONS.md`, `ASSUMPTIONS.md`, `OPEN_QUESTIONS.md`, `REJECTED_OPTIONS.md`

역할 구분:

```text
DECISIONS.md
- human-approved decisions only

ASSUMPTIONS.md
- useful but unverified working assumptions

OPEN_QUESTIONS.md
- unresolved questions that may affect later work

REJECTED_OPTIONS.md
- options that should not be revived unless explicitly reopened
```

---

## 9. Standard SKILL.md Structure

각 SKILL은 다음 구조를 권장한다.

```markdown
---
name: [[skill-name]]
description: [[When this skill should be used]]
stage: [[stage number and name]]
version: 1.0.0
status: draft
primary_output: [[path]]
requires_human_approval: true
---

# [[Skill Name]]

## 1. Purpose

## 2. When to Use

## 3. Required Inputs

## 4. Optional / Conditional Inputs

## 5. Files to Read First

## 6. USER_DIRECTIVES.md Handling

## 7. Input Preflight Procedure

## 8. Execution Procedure

## 9. Output Artifacts

## 10. Required Output Structure

## 11. Traceability Rules

## 12. Decision / Assumption / Open Question Rules

## 13. Validation Checklist

## 14. Human Approval Gate

## 15. Context Packet Update Rules

## 16. Do Not Do
```

Implementation-related SKILL에는 다음 addendum을 추가한다.

```markdown
## Implementation Addendum

- Inspect existing code before editing.
- Restate the task and allowed change scope.
- Identify or write the failing test first.
- Run the test and confirm failure if feasible.
- Implement the smallest change needed.
- Run relevant tests.
- Run broader regression tests if feasible.
- Record evidence.
- Update result and context files.
```

Review-related SKILL에는 다음 addendum을 추가한다.

```markdown
## Review Addendum

- Review against approved requirements.
- Review against acceptance criteria.
- Review against security and privacy constraints.
- Review against architecture and data decisions.
- Review test evidence.
- Identify release blockers.
- Separate blockers, warnings, and suggestions.
```

---

## 10. Standard SKILL Generation Procedure

LLM/Agent가 새로운 SKILL을 만들 때는 다음 절차를 따른다.

```text
1. Identify the target stage and step.
2. Read the core workflow concept document.
3. Read the core skill template.
4. Determine whether the skill is planning, design, implementation, review, or retrospective.
5. Define the skill-specific purpose and core question.
6. Define the stage folder.
7. Define Always Read inputs.
8. Define Read If Applicable inputs.
9. Define Do Not Read By Default inputs.
10. Define missing input handling.
11. Define mandatory output artifacts.
12. Define conditional output artifacts.
13. Define the output artifact structure.
14. Define traceability update rules.
15. Define decision, assumption, open question, and risk handling.
16. Define human approval gate.
17. Define context_packet.md update rules.
18. Add project-type specialization hooks.
19. Add tool-specific wrapper notes if needed.
20. Add validation checklist and anti-patterns.
```

---

## 11. Standard SKILL Runtime Procedure

Agent가 특정 SKILL을 실행할 때는 다음 절차를 따른다.

```text
1. Start from a clean or clearly bounded session if possible.
2. Read SKILL.md.
3. Read artifact_manifest.yml.
4. Read context_packet.md.
5. Read DECISIONS.md.
6. Check whether USER_DIRECTIVES.md exists in the stage folder.
7. If USER_DIRECTIVES.md exists, read it before executing the skill.
8. Confirm required inputs from the SKILL input contract.
9. Activate conditional inputs based on project profile and current context.
10. Verify existence and approval status of required inputs.
11. Report missing, draft, superseded, rejected, or conflicting inputs.
12. Restate the current task.
13. Identify missing or ambiguous information.
14. Produce or revise the primary artifact.
15. Produce conditional artifacts if applicable.
16. Update traceability if applicable.
17. Separate decision candidates, assumptions, open questions, and risks.
18. Update context_packet.md for the next stage.
19. Update ASSUMPTIONS.md, OPEN_QUESTIONS.md, REJECTED_OPTIONS.md as appropriate.
20. Do not update DECISIONS.md unless there is explicit human approval.
21. Request human review and approval.
```

---

## 12. Input Selection Rules

각 stage에서 어떤 이전 산출물을 사용할지는 다음 규칙으로 결정한다.

```text
Stage가 기본 입력을 결정한다.
시스템 유형이 조건부 입력을 결정한다.
직전 stage의 context_packet.md가 이번 실행의 실제 읽기 목록을 보정한다.
USER_DIRECTIVES.md가 stage-local 추가 지시를 제공한다.
최종적으로 preflight가 존재 여부, 승인 상태, 충돌 여부를 확인한다.
```

입력 우선순위는 다음과 같다.

```text
1. Current explicit user instruction
2. Stage-local USER_DIRECTIVES.md
3. APPROVAL_LOG.md / DECISIONS.md
4. artifact_manifest.yml
5. context_packet.md
6. Approved stage artifacts
7. Working assumptions
8. Agent inference
```

충돌이 있으면 Agent가 임의로 해결하지 않는다. 반드시 conflict로 보고한다.

---

## 13. Project Profiles

처음부터 모든 시스템 유형에 완벽히 맞는 SKILL을 만들려고 하지 않는다. 우선 다음 profile을 기준으로 설계한다.

```text
Profile A: Prototype / Research Tool
- lightweight artifacts
- fewer approval gates
- explicit assumptions allowed
- validation still required

Profile B: MVP Production
- most stages required
- test strategy required
- release readiness required
- security/privacy screening required

Profile C: Regulated / Security-Sensitive
- all critical stages required
- threat model required
- audit/privacy/compliance artifacts required
- stronger approval log required
- security tests and release blockers required
```

시스템 유형 addendum은 profile과 조합 가능해야 한다.

예시:

```text
web_saas + MVP Production
ai_data_product + Prototype
internal_tool + regulated_security_sensitive
mobile_app + brownfield_legacy
```

---

## 14. Stage Input Examples

### 14.1 Stage 4 Domain Modeling / DDD

```text
Always Read:
- /workflow/context/context_packet.md
- /workflow/context/DECISIONS.md
- /workflow/01_goal/01_service_goal.md
- /workflow/03_requirements/03_requirements.md
- /workflow/03_requirements/03_acceptance_criteria.md

Read If Applicable:
- /workflow/02_stakeholders_risk/02_risk_privacy_screening.md
  if roles, permissions, sensitive data, or compliance concerns affect domain rules

- /workflow/context/REJECTED_OPTIONS.md
  if previous modeling or scope options were rejected
```

---

### 14.2 Stage 8 Test Strategy & Validation Harness

```text
Always Read:
- /workflow/context/context_packet.md
- /workflow/context/DECISIONS.md
- /workflow/03_requirements/03_requirements.md
- /workflow/03_requirements/03_acceptance_criteria.md
- /workflow/05_architecture/05_architecture_plan.md
- /workflow/07_mvp_release/07_mvp_scope.md

Read If Applicable:
- /workflow/04_domain/04_business_rules_invariants.md
  if domain invariants require tests

- /workflow/05_architecture/05_api_contracts.md
  if APIs exist

- /workflow/06_data/06_data_security_rules.md
  if data access rules exist

- /workflow/00_intake/00_existing_context_review.md
  if this is a brownfield project
```

---

### 14.3 Stage 9 Task Breakdown

```text
Always Read:
- /workflow/03_requirements/03_requirements.md
- /workflow/03_requirements/03_acceptance_criteria.md
- /workflow/05_architecture/05_architecture_plan.md
- /workflow/07_mvp_release/07_mvp_scope.md
- /workflow/08_test_strategy/08_test_strategy.md
- /workflow/08_test_strategy/08_validation_commands.md

Read If Applicable:
- /workflow/04_domain/04_business_rules_invariants.md
- /workflow/05_architecture/05_api_contracts.md
- /workflow/06_data/06_data_security_rules.md
- /workflow/06_data/06_migration_plan.md
```

---

## 15. Anti-Patterns to Avoid

다음 방식은 피한다.

```text
- 시스템 유형별로 완전히 다른 common template을 여러 개 만든다.
- 모든 SKILL에 긴 common template 전체를 복사한다.
- 매번 이전 산출물을 읽고 SKILL.md 자체를 수정한다.
- 모든 이전 stage의 모든 파일을 읽게 한다.
- context_packet.md를 전체 history 저장소로 사용한다.
- context_packet.md만 source of truth로 사용한다.
- 승인되지 않은 agent output을 결정으로 취급한다.
- USER_DIRECTIVES.md의 모든 내용을 global decision으로 취급한다.
- missing information을 조용히 가정으로 바꾼다.
- rejected option을 다시 제안한다.
- implementation skill에서 test/evidence 없이 완료 보고한다.
- review skill에서 blocker, warning, suggestion을 구분하지 않는다.
```

---

## 16. Quality Checklist for SKILL Template Design

새로운 SKILL template을 만들 때 다음을 확인한다.

```text
[ ] Core template과 stage-specific 내용을 분리했다.
[ ] 이 SKILL이 답해야 하는 core question이 명확하다.
[ ] Always Read input이 정의되어 있다.
[ ] Conditional input이 정의되어 있다.
[ ] Do Not Read By Default가 정의되어 있다.
[ ] Missing input handling이 정의되어 있다.
[ ] Mandatory output artifact가 정의되어 있다.
[ ] Conditional output artifact가 정의되어 있다.
[ ] N/A record 규칙이 있다.
[ ] USER_DIRECTIVES.md 처리 규칙이 있다.
[ ] 승인된 결정과 agent 제안을 구분한다.
[ ] assumptions, open questions, risks를 분리한다.
[ ] traceability update 규칙이 있다.
[ ] context_packet.md update 규칙이 있다.
[ ] human approval gate가 있다.
[ ] implementation/review addendum이 필요한 경우 포함되어 있다.
[ ] tool-specific wrapper 내용이 core logic과 섞이지 않았다.
```

---

## 17. Initial Implementation Roadmap

처음부터 모든 것을 완벽하게 만들려고 하지 않는다. 다음 순서로 구현한다.

```text
1. Core Skill Template을 최소 형태로 재정리한다.
2. Stage 0~13에 대해 stage artifact contract를 정의한다.
3. Stage 0~13에 대해 1-stage-1-skill 버전을 먼저 만든다.
4. 너무 큰 stage만 3~5개의 smaller skill로 분할한다.
5. project profile addendum을 3~5개만 만든다.
6. Claude Code / Codex / Antigravity wrapper를 최소 수준으로 만든다.
7. 작은 실제 프로젝트에 적용한다.
8. agent failure pattern을 기록한다.
9. 실패 패턴을 template 개선 backlog로 전환한다.
10. 반복적으로 SKILL을 개선한다.
```

권장 초기 project profile:

```text
Greenfield MVP
Frontend + Backend + Database
Authentication 있음
개인정보 일부 있음
자동 테스트와 수동 검증 모두 필요
```

이 기준은 너무 단순하지도 않고, 너무 복잡하지도 않기 때문에 SKILL template 검증에 적합하다.

---

## 18. Instruction for LLM / Agent Designing SKILL Templates

LLM 또는 Agent에게 이 문서를 전달할 때 사용할 수 있는 지시문은 다음과 같다.

```text
You are designing reusable SKILL.md templates for a Manual Agentic Coding Workflow.

Follow these principles:

1. Do not create separate full common templates for each system type.
2. Create a small Core Skill Template and specialize it by stage.
3. Use project-type specialization addenda for system-specific concerns.
4. Use tool-specific wrappers only for execution environment differences.
5. Each SKILL must define its input contract: Always Read, Read If Applicable, Do Not Read By Default, and Missing Input Handling.
6. Each SKILL must define its output artifact contract: Mandatory Artifacts, Conditional Artifacts, N/A Record, and Context Packet Update Rules.
7. Do not require the user to rewrite SKILL.md for every project.
8. Project-specific information must come from approved artifacts, context_packet.md, artifact_manifest.yml, and USER_DIRECTIVES.md.
9. context_packet.md is a navigation layer, not the sole source of truth.
10. Only human-approved decisions may be recorded as decisions.
11. Agent assumptions must remain assumptions until confirmed.
12. Every stage must prepare the next stage by updating context_packet.md with only the minimum required context.
13. Every implementation task must produce test or validation evidence.
14. Every review task must separate blockers, warnings, and suggestions.
15. Design SKILLs so that a new agent session can start from files only, without relying on previous chat history.
```

---

## 19. Final Principle

가장 중요한 원칙은 다음이다.

```text
Template은 작업 방식을 표준화한다.
Stage-specific SKILL은 판단 내용을 구체화한다.
Project specialization은 시스템 유형별 추가 요구를 반영한다.
Tool wrapper는 실행 환경 차이만 처리한다.
Artifact와 approval log가 stage 간 source of truth를 제공한다.
```

따라서 SKILL template 체계는 다음 목표를 만족해야 한다.

```text
Reusable
Inspectable
Artifact-first
Human-approved
Traceable
Context-reset tolerant
Production-aware
```
