# MISSION.md
v0.1
2026-06-23

## Metadata

- Project ID: AI Software Studio
- Mission ID: MISSION-UX-DESIGNER-INTEGRATION
- Version: v0.1
- Creation Date: 2026-06-23
- Author: Studio Director
- Source Artifacts:
  - `ideas/roadmap_ux.md`
  - `documents/STUDIO_IMPROVEMENT_PROCESS.md`
  - `documents/LIFECYCLE.md`
  - `documents/ARTIFACTS.md`
  - `documents/AGENTS.md`
  - `documents/DECISION_AUTHORITY.md`
- Source Of Work:
  - Source: `ideas/roadmap_ux.md`
  - Source Type: Roadmap
  - Source Reference: UX Designer Integration
  - Trace: Studio Evolution -> UX Designer Roadmap -> Mission Program

## Mission Summary

- Title: UX Designer Integration Program
- Goal: Полностью внедрить UX Designer в AI Software Studio.
- Description: Mission добавляет UX Designer как каноническую роль, встраивает UX Design в основной производственный цикл, описывает UX Artifacts, UX Review Mode, UX Finding как Source Of Work candidate и интеграцию UX Review в Mission Mode.
- Expected Outcome: Студия может запустить отдельную миссию `Провести UX Review Idle Math Lab` и выполнить её через UX Designer без привлечения других ролей как UX-экспертов.

## Mission Boundaries

- In Scope:
  - Документация AI Software Studio.
  - Новая роль UX Designer.
  - UX Design lifecycle stage.
  - UX Review Mode.
  - UX Requirements, UX Risks and UX Review artifacts.
  - UX Finding as Source Of Work candidate after Product Owner Review.
  - Mission Mode UX Review hook after milestone, release or roadmap stage.
  - UX Integration Review.
- Out Of Scope:
  - Изменение существующих игровых проектов.
  - Изменение Idle Math Lab.
  - Изменение существующих Mission histories.
  - Создание дополнительных ролей помимо UX Designer.
  - Изменение Mission Mode v0.2 autonomy model.
  - Решения Product Owner по конкретным UX Findings.
- Scope Protection:
  - Mission меняет только канонические документы Студии и новые mission artifacts этой программы.
  - UX Designer не получает полномочия над game mechanics, balance, core loop, rewards, retention, game economy, business logic, architecture or code.
  - UX Finding не становится Backlog item без Product Owner Review.

## Stage Missions

- Stage Mission 1: Responsibility Boundary
  - Roadmap Stage: Stage 1. Определение зоны ответственности.
  - Owner: Studio Director -> UX Designer documentation.
  - Expected Output: UX Designer has unique responsibility without overlap with Product Analyst.
- Stage Mission 2: Production Cycle Integration
  - Roadmap Stage: Stage 2. Встраивание в производственный цикл.
  - Owner: Studio Director -> Product Analyst, UX Designer, Product Owner, Solution Architect handoff docs.
  - Expected Output: Product Analyst -> UX Designer -> Product Owner -> Solution Architect chain is documented.
- Stage Mission 3: UX Artifacts
  - Roadmap Stage: Stage 3. UX Artifacts.
  - Owner: UX Designer / ARTIFACTS.md.
  - Expected Output: `UX_REVIEW.md`, `UX_REQUIREMENTS.md`, `UX_RISKS.md` are canonical artifact types.
- Stage Mission 4: UX Review Mode
  - Roadmap Stage: Stage 4. UX Review Mode.
  - Owner: UX Designer.
  - Expected Output: UX Review inputs, outputs, findings, severity and recommendations are documented.
- Stage Mission 5: UX Source Of Work
  - Roadmap Stage: Stage 5. UX Source Of Work.
  - Owner: Product Owner and Delivery Planner boundaries.
  - Expected Output: UX Finding can become Source Of Work only after Product Owner Review.
- Stage Mission 6: Mission Mode Integration
  - Roadmap Stage: Stage 6. Mission Mode Integration.
  - Owner: Studio Director.
  - Expected Output: Mission Mode can call UX Review after milestone, release or roadmap stage without changing Mission Mode v0.2.

## Mission Run Policy

- Mission Run Authorization Required: Yes
- Mission Run Artifact: `documents/missions/MISSION-UX-DESIGNER-INTEGRATION/runs/<RUN_ID>/MISSION_RUN.md`
- Allowed Mission Run Scope: Documentation changes in AI Software Studio and mission artifacts for this program.
- Run-Specific Parameters Location: `MISSION_RUN.md`
- Authorization Owner: Studio Director
- Allowed Autonomy Level: Bounded Multi-Cycle Mission

## Mission-Level Budget Policy

- Budget Ownership: Mission Run.
- Run Budget Location: `documents/missions/MISSION-UX-DESIGNER-INTEGRATION/runs/<RUN_ID>/MISSION_RUN.md`
- Concrete Typed Budget: Must be defined in `MISSION_RUN.md`.
- Mission-Level Guardrails:
  - Maximum roadmap scope: UX Designer Roadmap Stage 1 through Stage 6.
  - Maximum new canonical roles: 1, UX Designer.
  - Maximum project implementation files changed: 0.
  - Existing mission histories must remain untouched.
  - Stop if any roadmap stage requires Product Owner decision or Mission Mode v0.2 change.

## Stop Conditions

- требуется изменение архитектуры ролей за пределами roadmap;
- требуется изменение Mission Mode v0.2;
- требуется создание дополнительных ролей помимо UX Designer;
- возникают противоречия между UX Designer и существующими ролями;
- требуется решение Product Owner;
- изменение затрагивает существующие игровые проекты или Idle Math Lab;
- изменение затрагивает существующие Mission histories.

## Completion Criteria

- Criterion: UX Designer exists as a canonical role.
  - Verification Method: `documents/AGENTS.md` and `documents/agents/UX_DESIGNER.md` define the role.
  - Source: `ideas/roadmap_ux.md`, Stage 1.
- Criterion: UX Designer is integrated into the main cycle.
  - Verification Method: `documents/LIFECYCLE.md` contains UX DESIGN between DISCOVERY and PRODUCT DEFINITION.
  - Source: `ideas/roadmap_ux.md`, Stage 2.
- Criterion: UX artifacts are described.
  - Verification Method: `documents/ARTIFACTS.md` defines `UX_REQUIREMENTS.md`, `UX_RISKS.md` and `UX_REVIEW.md`.
  - Source: `ideas/roadmap_ux.md`, Stage 3.
- Criterion: UX Review Mode exists.
  - Verification Method: `documents/agents/UX_DESIGNER.md` and `documents/ARTIFACTS.md` define UX Review.
  - Source: `ideas/roadmap_ux.md`, Stage 4.
- Criterion: UX Findings can become Source Of Work.
  - Verification Method: `ARTIFACTS.md`, `DELIVERY_PLANNER.md` and `CODEX_TASK_FORMULATION_PROCESS.md` define UX Finding trace after Product Owner Review.
  - Source: `ideas/roadmap_ux.md`, Stage 5.
- Criterion: Mission Mode can use UX Review.
  - Verification Method: `LIFECYCLE.md` and `STUDIO_DIRECTOR.md` describe UX Review hook after milestone, release or roadmap stage.
  - Source: `ideas/roadmap_ux.md`, Stage 6.
- Criterion: Final UX Integration Review exists.
  - Verification Method: `UX_INTEGRATION_REVIEW.md` exists and confirms launch readiness for `Провести UX Review Idle Math Lab`.
  - Source: Mission expected result.

## Assumptions

- The roadmap named in the launch request as `ROADMAP_UX.md` corresponds to the existing file `ideas/roadmap_ux.md`.
- The user launch request is treated as explicit authorization for this Studio Improvement Mission.
- `Mission Mode v0.2` means the current autonomy, typed budget and run authorization model must not be replaced.

## Known Risks

- Adding a new lifecycle stage can make older examples stale. This Mission updates README and Studio Director lifecycle summary, but existing historical mission records remain unchanged by scope.
- UX Designer must not become a hidden Product Owner. Product Owner Review remains required before UX Finding becomes Source Of Work.
