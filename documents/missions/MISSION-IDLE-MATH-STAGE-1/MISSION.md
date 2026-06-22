# MISSION.md
v0.1
2026-06-22

## Metadata

- Project ID: Idle Math Lab
- Mission ID: MISSION-IDLE-MATH-STAGE-1
- Version: v0.1
- Creation Date: 2026-06-22
- Author: Studio Director
- Source Artifacts:
  - `ideas/roadmap_v03_mission_mode.md`
  - `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
  - `documents/ARTIFACTS.md`
  - `documents/LIFECYCLE.md`
  - `documents/AGENTS.md`
- Source Of Work:
  - Source: `ideas/roadmap_v03_mission_mode.md`
  - Source Type: Roadmap
  - Source Reference: `roadmap_v03_mission_mode.md`
  - Trace: Mission Mode v03 -> Pilot Mission -> Mission Framework

## Mission Summary

- Title: Idle Math Lab Stage 1 Technical Foundation
- Goal: Завершить Stage 1 roadmap Idle Math Lab.
- Description: Mission закрепляет долгоживущий объект работы для пилотной проверки Mission Mode на Idle Math Lab. Mission охватывает только Stage 1 Technical Foundation и подготавливает состояние, backlog и review-цикл без автоматического запуска реализации.
- Expected Outcome: Stage 1 Technical Foundation завершён: экономика и сохранение вынесены из `GameEngine`, pure logic покрыта XCTest target, ключевые gameplay ids централизованы, базовая testability foundation готова для будущих изменений.

## Mission Boundaries

- In Scope:
  - Stage 1: Technical Foundation из Idle Math Lab roadmap.
  - Mission state tracking.
  - Mission-specific backlog для Stage 1.
  - Review-ready стартовое состояние Mission.
  - Следующие задачи только на уровне Mission Backlog, без детальных Task Specifications.
- Out Of Scope:
  - Stage 2 Readability and UX.
  - Proof Preview Pass.
  - Research Section Readability Pass.
  - Dynamic Research Determinism and Generator Tests.
  - Formula Economy Explanation UI.
  - Любые новые игровые механики.
  - Автоматическое выполнение задач Mission.
- Scope Protection:
  - Mission не расширяет roadmap Idle Math Lab.
  - Mission не меняет vision игры.
  - Mission не добавляет крупные функции вне Stage 1.
  - Mission не меняет продуктовую стратегию.
  - Новые идеи фиксируются как Opportunity и требуют решения Product Owner.
- Forbidden Changes:
  - Не менять исходный код Idle Math Lab в рамках Mission Framework.
  - Не создавать Task Specifications на этом шаге.
  - Не запускать Implementation Loop.
  - Не запускать Autonomous Loop.
  - Не добавлять новые роли.

## Input Artifacts

- Artifact or Input: Mission Mode roadmap
  - Path or Reference: `ideas/roadmap_v03_mission_mode.md`
  - Role In Mission: Source Of Work для пилотной Mission.
  - Status: Available
  - Limitations: None
- Artifact or Input: Idle Math Lab roadmap
  - Path or Reference: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
  - Role In Mission: Источник Stage 1 Technical Foundation и порядка backlog items.
  - Status: Available
  - Limitations: В `ideas/roadmap_v03_mission_mode.md` пилотная ссылка названа `IDLE_MATH_LAB_REVIEW_AND_ROADMAP.md`; в текущем filesystem найден фактический файл `IDLE_MATH_LAB_ROADMAP.md`.
- Artifact or Input: Current Idle Math Lab working tree
  - Path or Reference: `/Users/sa/Documents/codex/ios/Idle Math Lab`
  - Role In Mission: Evidence для уже выполненных foundation changes.
  - Status: Available
  - Limitations: Есть незакоммиченные изменения в соседнем проекте Idle Math Lab; Mission Framework их не изменяет.
- Artifact or Input: Studio Mission Mode documentation
  - Path or Reference: `documents/LIFECYCLE.md`, `documents/ARTIFACTS.md`, `documents/AGENTS.md`, `documents/ROLE_EXECUTION_RULES.md`
  - Role In Mission: Правила Mission lifecycle, artifacts, roles, traceability, budget and stop conditions.
  - Status: Available
  - Limitations: Step 1 documentation changes are present in the current working tree.

## Mission Lifecycle

- Mission Intake:
  - Purpose: Зафиксировать пилотную Mission и её основание.
  - Inputs: `ideas/roadmap_v03_mission_mode.md`, Idle Math Lab roadmap, request for Pilot Mission Framework.
  - Outputs: `MISSION.md`.
  - Responsible Role: Studio Director.
- Mission Planning:
  - Purpose: Определить scope, milestone, budget автономности, stop conditions и completion criteria.
  - Inputs: `MISSION.md`, Idle Math Lab roadmap, current project state evidence.
  - Outputs: `MISSION_STATE.md`.
  - Responsible Role: Studio Director.
- Backlog Generation:
  - Purpose: Сформировать Mission-level backlog Stage 1 без детальных Task Specifications.
  - Inputs: Idle Math Lab roadmap Stage 1, completed pre-mission work evidence.
  - Outputs: `MISSION_BACKLOG.md`.
  - Responsible Role: Delivery Planner.
- Implementation Loop:
  - Purpose: В будущих шагах выполнять обычные Task через Task Mode.
  - Inputs: Mission Backlog item, Task Specification, Source Of Work trace.
  - Outputs: Implementation Reports and Validation Reports.
  - Responsible Role: Delivery Planner, Implementer, Validator.
- Mission Review:
  - Purpose: Проверять состояние Mission после цикла, milestone, blocker or budget event.
  - Inputs: Mission State, Mission Backlog, Implementation Reports, Validation Reports.
  - Outputs: `MISSION_REVIEW.md`.
  - Responsible Role: Studio Director.
- Mission Complete:
  - Purpose: Завершить Mission после выполнения Stage 1 или остановки по stop condition.
  - Inputs: Mission Review, Mission State, Mission Backlog, validation evidence.
  - Outputs: Final Mission Review, updated Mission State, Project Memory update request if needed.
  - Responsible Role: Studio Director and Historian.

## Milestones

- Milestone: Stage 1 — Technical Foundation
  - Completion Criteria:
    - `GameEngine.swift` больше не содержит полную формулу tap/passive/proof.
    - `GameEngine` не вызывает `UserDefaults` напрямую.
    - Есть XCTest target для pure logic.
    - Есть тесты на income, Proof reward, offline cap, state decoding and theorem allocation.
    - Ключевые gameplay ids централизованы в `GameIDs.swift` или эквивалентном типизированном источнике.
    - Debug Reset, quit/reopen, tap, passive income and Proof продолжают работать.
  - Related Source: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`, Stage 1: Technical Foundation.
  - Expected Tasks:
    - EconomySnapshot and Income Breakdown.
    - GameSaveStore with Versioned Save.
    - Add XCTest Target for Pure Logic.
    - Add base pure-logic test coverage.
    - Centralize Gameplay IDs.

## Autonomy Budget

- Task Limit: Maximum 5 implementation tasks in a row.
- Cycle Limit: Maximum 3 Mission Review cycles before explicit review by Studio Director.
- File Change Limit: Maximum 25 changed files across the active Mission implementation loop.
- Time Limit: Not set for this framework step.
- Other Limits:
  - Maximum 1 roadmap stage: Stage 1 Technical Foundation.
  - Stop after Stage 1 milestone completion.
  - No autonomous execution during Mission Framework creation.
  - Single-Step Mode: one Mission run may execute only one backlog item.
- Budget Exhaustion Rule: If any budget limit is reached, Mission must stop and prepare `MISSION_REVIEW.md` before further implementation.

## Stop Conditions

- требуется продуктовое решение;
- найден архитектурный блокер;
- roadmap противоречит проекту;
- есть несколько равноценных направлений развития;
- достигнут milestone Stage 1 — Technical Foundation;
- исчерпан бюджет автономности;
- следующая работа выходит за Stage 1 roadmap;
- следующая работа требует изменения vision, product strategy or major feature scope.

## Completion Criteria

- Criterion: Mission Definition exists.
  - Verification Method: `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION.md` exists and contains Mission ID, goal, boundaries, budget and stop conditions.
  - Source: Mission Mode v03 -> Pilot Mission.
- Criterion: Mission State exists.
  - Verification Method: `MISSION_STATE.md` records created/not-started status and completed pre-mission work.
  - Source: Mission Mode v03 -> Mission Artifacts.
- Criterion: Mission Backlog exists.
  - Verification Method: `MISSION_BACKLOG.md` contains Stage 1 backlog items with Source Of Work and trace.
  - Source: Idle Math Lab roadmap Stage 1.
- Criterion: Mission Review exists.
  - Verification Method: `MISSION_REVIEW.md` contains startup review, risks, remaining work and next step.
  - Source: Mission lifecycle -> Mission Review.
- Criterion: Autonomous Loop is not running.
  - Verification Method: No Task Specifications are created and no implementation is launched as part of this step.
  - Source: User task constraints.

## Assumptions

- `EconomySnapshot` / `EconomyCalculator` and `GameSaveStore` are treated as completed pre-mission work because the user explicitly instructed to use them as already completed work and the adjacent Idle Math Lab working tree contains those files.
- Automated validation for completed pre-mission work is not yet available because XCTest target is still absent.
- `IDLE_MATH_LAB_ROADMAP.md` is the current filesystem equivalent of the roadmap referenced in Mission Mode v03 as `IDLE_MATH_LAB_REVIEW_AND_ROADMAP.md`.

## Known Risks

- Completed pre-mission work is visible in an uncommitted adjacent project working tree; Mission must not assume release readiness until Validator checks it.
- No XCTest target exists yet, so Stage 1 cannot be considered complete.
- Gameplay IDs are still not centralized in `GameIDs.swift`.
- If adding tests exposes defects in completed pre-mission work, Mission should route rework through normal Task Mode.

## Pilot Reference

- Pilot Mission ID: MISSION-IDLE-MATH-STAGE-1
- Pilot Goal: Завершить Stage 1 из Idle Math Lab roadmap.
- Autonomous Loop Status: Not Started
- Single-Step Loop Status: Defined; not executed
- Next Backlog Item: MISSION-IDLE-MATH-STAGE-1-T003 — Add XCTest Target for Pure Logic
