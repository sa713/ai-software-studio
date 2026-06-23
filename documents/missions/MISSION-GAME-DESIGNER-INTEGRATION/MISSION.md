# MISSION.md
v0.1
2026-06-23

## Metadata

- Project ID: AI Software Studio
- Mission ID: MISSION-GAME-DESIGNER-INTEGRATION
- Version: v0.1
- Creation Date: 2026-06-23
- Author: Studio Director
- Source Artifacts:
  - `ideas/roadmap_game.md`
  - `documents/STUDIO_IMPROVEMENT_PROCESS.md`
  - `documents/LIFECYCLE.md`
  - `documents/ARTIFACTS.md`
  - `documents/AGENTS.md`
  - `documents/DECISION_AUTHORITY.md`
- Source Of Work:
  - Source: `ideas/roadmap_game.md`
  - Source Type: Roadmap
  - Source Reference: Game Designer Integration
  - Trace: Studio Evolution -> Game Designer Roadmap -> Mission Program

## Mission Summary

- Title: Game Designer Integration Program
- Goal: Полностью внедрить Game Designer в AI Software Studio.
- Description: Mission добавляет Game Designer как каноническую роль для игровых проектов, встраивает Game Design в production lifecycle, описывает Game Design Artifacts, Game Design Review Mode, Gameplay Finding как Source Of Work candidate и интеграцию Game Design Review в Mission Mode.
- Expected Outcome: Студия может запустить отдельную миссию `Провести Game Design Review Idle Math Lab` и выполнить её через Game Designer без подмены этих функций Product Analyst, Product Owner, UX Designer or Validator.

## Mission Boundaries

- In Scope:
  - Документация AI Software Studio.
  - Новая роль Game Designer.
  - Game Design lifecycle stage for game projects.
  - Game Design Review Mode.
  - Core Loop Review, Progression Review, Reward Review and Retention Review.
  - `GAME_DESIGN_REVIEW.md`, `GAME_DESIGN_NOTES.md`, `GAMEPLAY_RISKS.md`, `GAMEPLAY_OPPORTUNITIES.md`.
  - Gameplay Finding as Source Of Work candidate after Product Owner Review.
  - Mission Mode Game Design Review hook after roadmap stage, economy change, progression change or product completion.
  - Game Designer Integration Review.
- Out Of Scope:
  - Изменение существующих игровых проектов.
  - Изменение Idle Math Lab.
  - Изменение существующих Mission histories.
  - Изменение UX Designer roadmap и его результатов без необходимости.
  - Создание дополнительных игровых ролей.
  - Изменение Mission Mode v0.2 autonomy model.
  - Решения Product Owner по конкретным Gameplay Findings.
- Scope Protection:
  - Mission меняет только канонические документы Студии и новые mission artifacts этой программы.
  - Game Designer не получает полномочия над UI layout, навигацией, визуальным дизайном, архитектурой, реализацией, кодом or Validation.
  - Gameplay Finding не становится Backlog item без Product Owner Review.
  - Product Owner retains product goals, product priority, backlog acceptance and final product authority.

## Stage Missions

- Stage Mission 1: Responsibility Definition
  - Roadmap Stage: Stage 1. Определение зоны ответственности.
  - Owner: Studio Director -> Game Designer documentation.
  - Expected Output: Game Designer owns gameplay experience and does not overlap with UX Designer, Product Owner, Solution Architect or Validator.
- Stage Mission 2: Production Integration
  - Roadmap Stage: Stage 2. Встраивание в производственный цикл.
  - Owner: Studio Director -> role handoff docs.
  - Expected Output: Product Analyst -> UX Designer -> Product Owner -> Game Designer -> Solution Architect -> Delivery Planner chain is documented for game projects.
- Stage Mission 3: Game Design Artifacts
  - Roadmap Stage: Stage 3. Game Design Artifacts.
  - Owner: Game Designer / ARTIFACTS.md.
  - Expected Output: `GAME_DESIGN_REVIEW.md`, `GAME_DESIGN_NOTES.md`, `GAMEPLAY_RISKS.md` and `GAMEPLAY_OPPORTUNITIES.md` are canonical artifact types.
- Stage Mission 4: Review Mode
  - Roadmap Stage: Stage 4. Game Design Review Mode.
  - Owner: Game Designer.
  - Expected Output: Game Design Review inputs, outputs, findings, severity and recommendations are documented.
- Stage Mission 5: Gameplay Findings
  - Roadmap Stage: Stage 5. Gameplay Findings.
  - Owner: Product Owner and Delivery Planner boundaries.
  - Expected Output: Gameplay Finding can become Source Of Work only after Product Owner Review.
- Stage Mission 6: Specialized Reviews
  - Roadmap Stage: Stage 6. Balance & Progression Reviews / Specialized Reviews.
  - Owner: Game Designer.
  - Expected Output: Core Loop Review, Progression Review, Reward Review and Retention Review are documented as specialized Game Design Review types.
- Stage Mission 7: Mission Mode Integration
  - Roadmap Stage: Stage 7. Mission Mode Integration.
  - Owner: Studio Director.
  - Expected Output: Mission Mode can call Game Design Review without changing Mission Mode v0.2.

## Mission Run Policy

- Mission Run Authorization Required: Yes
- Mission Run Artifact: `documents/missions/MISSION-GAME-DESIGNER-INTEGRATION/runs/<RUN_ID>/MISSION_RUN.md`
- Allowed Mission Run Scope: Documentation changes in AI Software Studio and mission artifacts for this program.
- Run-Specific Parameters Location: `MISSION_RUN.md`
- Authorization Owner: Studio Director
- Allowed Autonomy Level: Bounded Multi-Cycle Mission

## Mission-Level Budget Policy

- Budget Ownership: Mission Run.
- Run Budget Location: `documents/missions/MISSION-GAME-DESIGNER-INTEGRATION/runs/<RUN_ID>/MISSION_RUN.md`
- Concrete Typed Budget: Must be defined in `MISSION_RUN.md`.
- Mission-Level Guardrails:
  - Maximum roadmap scope: Game Designer Roadmap Stage 1 through Stage 7.
  - Maximum new canonical roles: 1, Game Designer.
  - Maximum project implementation files changed: 0.
  - Existing mission histories must remain untouched.
  - UX Designer roadmap and results must remain untouched unless directly required for role boundary consistency.
  - Stop if any roadmap stage requires Product Owner decision or Mission Mode v0.2 change.

## Stop Conditions

- требуется изменение Mission Mode v0.2;
- требуется изменение UX Designer roadmap;
- требуется создание дополнительных игровых ролей;
- возникает конфликт полномочий между Product Owner и Game Designer;
- требуется решение Product Owner;
- изменение затрагивает существующие игровые проекты или Idle Math Lab;
- изменение затрагивает существующие Mission histories.

## Completion Criteria

- Criterion: Game Designer exists as a canonical role.
  - Verification Method: `documents/AGENTS.md` and `documents/agents/GAME_DESIGNER.md` define the role.
  - Source: `ideas/roadmap_game.md`, Stage 1.
- Criterion: Game Designer is integrated into the production cycle for game projects.
  - Verification Method: `documents/LIFECYCLE.md` contains GAME DESIGN after PRODUCT DEFINITION and before SOLUTION DESIGN for game projects.
  - Source: `ideas/roadmap_game.md`, Stage 2.
- Criterion: Game Design artifacts are described.
  - Verification Method: `documents/ARTIFACTS.md` defines `GAME_DESIGN_REVIEW.md`, `GAME_DESIGN_NOTES.md`, `GAMEPLAY_RISKS.md` and `GAMEPLAY_OPPORTUNITIES.md`.
  - Source: `ideas/roadmap_game.md`, Stage 3.
- Criterion: Game Design Review Mode exists.
  - Verification Method: `documents/agents/GAME_DESIGNER.md`, `documents/LIFECYCLE.md` and `documents/ARTIFACTS.md` define Game Design Review.
  - Source: `ideas/roadmap_game.md`, Stage 4.
- Criterion: Gameplay Findings can become Source Of Work.
  - Verification Method: `ARTIFACTS.md`, `DELIVERY_PLANNER.md` and `CODEX_TASK_FORMULATION_PROCESS.md` define Gameplay Finding trace after Product Owner Review.
  - Source: `ideas/roadmap_game.md`, Stage 5.
- Criterion: Specialized reviews exist.
  - Verification Method: `GAME_DESIGNER.md` and `ARTIFACTS.md` define Core Loop Review, Progression Review, Reward Review and Retention Review.
  - Source: `ideas/roadmap_game.md`, Stage 6.
- Criterion: Mission Mode can use Game Design Review.
  - Verification Method: `LIFECYCLE.md` and `STUDIO_DIRECTOR.md` describe Game Design Review hook after roadmap stage, economy change, progression change or product completion.
  - Source: `ideas/roadmap_game.md`, Stage 7.
- Criterion: Final Game Designer Integration Review exists.
  - Verification Method: `GAME_DESIGNER_INTEGRATION_REVIEW.md` exists and confirms launch readiness for `Провести Game Design Review Idle Math Lab`.
  - Source: Mission expected result.

## Assumptions

- The roadmap named in the launch request as `ROADMAP_GAME.md` corresponds to the existing file `ideas/roadmap_game.md`.
- The user launch request is treated as explicit authorization for this Studio Improvement Mission.
- `Mission Mode v0.2` means the current autonomy, typed budget and run authorization model must not be replaced.
- Game Design applies only to game projects; non-game projects skip GAME DESIGN unless explicitly authorized by Studio Director.

## Known Risks

- Adding a new lifecycle stage can make older examples stale. This Mission updates canonical lifecycle and role documents, but existing historical mission records remain unchanged by scope.
- Game Designer must not become a hidden Product Owner. Product Owner Review remains required before Gameplay Finding becomes Source Of Work.
- Game Designer must not replace UX Designer. UI layout, navigation and usability remain UX-owned.
