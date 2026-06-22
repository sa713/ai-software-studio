# MISSION_BACKLOG.md
v0.1
2026-06-22

## Metadata

- Project ID: Idle Math Lab
- Mission ID: MISSION-IDLE-MATH-STAGE-1
- Version: v0.1
- Creation Date: 2026-06-22
- Author: Delivery Planner
- Source Artifacts:
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION.md`
  - `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
  - `ideas/roadmap_v03_mission_mode.md`
- Mission Definition: `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION.md`

## Mission Work Summary

- Mission Goal: Завершить Stage 1 — Technical Foundation из Idle Math Lab roadmap.
- Execution Strategy: Использовать уже выполненные EconomySnapshot/EconomyCalculator и GameSaveStore как pre-mission foundation, затем добавить XCTest target, покрыть pure logic тестами и централизовать gameplay ids.
- Key Dependencies:
  - XCTest target depends on current pure logic surfaces: `EconomyCalculator`, `EconomySnapshot`, `GameSaveStore`, `GameState`, `TheoremAllocation`.
  - Gameplay IDs should follow after tests or alongside testability checks to avoid behavior drift.
  - Stage 1 completion depends on validation evidence, not only code presence.
- Known Risks:
  - Automated tests are currently absent.
  - Completed pre-mission work is visible in an adjacent uncommitted working tree.
  - `GameIDs.swift` is not present yet.

## Mission Tasks

- Task ID: MISSION-IDLE-MATH-STAGE-1-T001
  - Title: EconomySnapshot and Income Breakdown
  - Source Of Work:
    - Source: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
    - Source Type: Roadmap
    - Source Reference: Stage 1 Technical Foundation; Immediate Implementation Queue item 1
    - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 → Roadmap: Idle Math Lab Stage 1 Technical Foundation → Backlog Item: EconomySnapshot and Income Breakdown
  - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 → Roadmap: Stage 1 Technical Foundation → Backlog Item: MISSION-IDLE-MATH-STAGE-1-T001
  - Description: Extract economy calculation from `GameEngine.swift` into `EconomyCalculator` and return `EconomySnapshot`.
  - Owner: Implementer
  - Related Mission Milestone: Stage 1 — Technical Foundation
  - Related Roadmap / Review / Backlog Item: `EconomySnapshot and Income Breakdown`
  - Dependencies: None
  - Status: Done
  - Status Notes: Completed before Mission Framework creation.
  - Stop Condition Risk: None

- Task ID: MISSION-IDLE-MATH-STAGE-1-T002
  - Title: GameSaveStore with Versioned Save
  - Source Of Work:
    - Source: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
    - Source Type: Roadmap
    - Source Reference: Stage 1 Technical Foundation; Immediate Implementation Queue item 2
    - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 → Roadmap: Idle Math Lab Stage 1 Technical Foundation → Backlog Item: GameSaveStore with Versioned Save
  - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 → Roadmap: Stage 1 Technical Foundation → Backlog Item: MISSION-IDLE-MATH-STAGE-1-T002
  - Description: Extract save/load/reset from `GameEngine` into `GameSaveStore` and preserve legacy save behavior.
  - Owner: Implementer
  - Related Mission Milestone: Stage 1 — Technical Foundation
  - Related Roadmap / Review / Backlog Item: `GameSaveStore with Versioned Save`
  - Dependencies:
    - MISSION-IDLE-MATH-STAGE-1-T001, because save tests should use stable state/economy assumptions.
  - Status: Done
  - Status Notes: Completed before Mission Framework creation.
  - Stop Condition Risk: None

- Task ID: MISSION-IDLE-MATH-STAGE-1-T003
  - Title: Add XCTest Target for Pure Logic
  - Source Of Work:
    - Source: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
    - Source Type: Roadmap
    - Source Reference: Stage 1 Technical Foundation; Immediate Implementation Queue item 3
    - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 → Roadmap: Idle Math Lab Stage 1 Technical Foundation → Backlog Item: Add XCTest Target for Pure Logic
  - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 → Roadmap: Stage 1 Technical Foundation → Backlog Item: MISSION-IDLE-MATH-STAGE-1-T003
  - Description: Add an iOS XCTest target for pure logic so economy, persistence, state decoding and theorem allocation can be tested without UI.
  - Owner: Delivery Planner -> Implementer
  - Related Mission Milestone: Stage 1 — Technical Foundation
  - Related Roadmap / Review / Backlog Item: `Add XCTest Target for Pure Logic`
  - Dependencies:
    - MISSION-IDLE-MATH-STAGE-1-T001
    - MISSION-IDLE-MATH-STAGE-1-T002
  - Status: Ready
  - Status Notes: Selected next backlog item for Single-Step Loop; implementation not started.
  - Stop Condition Risk: Architecture blocker if current Xcode project structure cannot support a test target without project regeneration.

- Task ID: MISSION-IDLE-MATH-STAGE-1-T004
  - Title: Add Base Pure Logic Test Coverage
  - Source Of Work:
    - Source: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
    - Source Type: Roadmap
    - Source Reference: Stage 1 criteria: income, Proof reward, offline cap, state decoding and theorem allocation tests
    - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 → Roadmap: Idle Math Lab Stage 1 Technical Foundation → Backlog Item: Base pure logic tests
  - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 → Roadmap: Stage 1 Technical Foundation → Backlog Item: MISSION-IDLE-MATH-STAGE-1-T004
  - Description: Add first tests for `EconomyCalculator`, `EconomySnapshot`, `GameSaveStore`, `GameState` decoding/default behavior, offline cap and `TheoremAllocation`.
  - Owner: Delivery Planner -> Implementer
  - Related Mission Milestone: Stage 1 — Technical Foundation
  - Related Roadmap / Review / Backlog Item: Stage 1 readiness criteria and Immediate Implementation Queue item 3
  - Dependencies:
    - MISSION-IDLE-MATH-STAGE-1-T003
  - Status: Planned
  - Stop Condition Risk: Product risk if tests expose behavior ambiguity that requires a product decision about balance.

- Task ID: MISSION-IDLE-MATH-STAGE-1-T005
  - Title: Centralize Gameplay IDs
  - Source Of Work:
    - Source: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
    - Source Type: Roadmap
    - Source Reference: Stage 1 Technical Foundation; Immediate Implementation Queue item 6
    - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 → Roadmap: Idle Math Lab Stage 1 Technical Foundation → Backlog Item: Centralize Gameplay IDs
  - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 → Roadmap: Stage 1 Technical Foundation → Backlog Item: MISSION-IDLE-MATH-STAGE-1-T005
  - Description: Add constants or typed IDs for key upgrade/focus/paradigm/function/project identifiers and replace the highest-risk duplicated string literals.
  - Owner: Delivery Planner -> Implementer
  - Related Mission Milestone: Stage 1 — Technical Foundation
  - Related Roadmap / Review / Backlog Item: `Centralize Gameplay IDs`
  - Dependencies:
    - MISSION-IDLE-MATH-STAGE-1-T003
    - MISSION-IDLE-MATH-STAGE-1-T004, recommended before wide replacement if behavior checks are needed.
  - Status: Planned
  - Stop Condition Risk: Scope risk if replacement grows beyond key gameplay ids into broad content refactor.

- Task ID: MISSION-IDLE-MATH-STAGE-1-T006
  - Title: Stage 1 Completion Review
  - Source Of Work:
    - Source: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
    - Source Type: Roadmap
    - Source Reference: Stage 1 completion criteria
    - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 → Roadmap: Idle Math Lab Stage 1 Technical Foundation → Backlog Item: Stage 1 completion criteria
  - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 → Roadmap: Stage 1 Technical Foundation → Backlog Item: MISSION-IDLE-MATH-STAGE-1-T006
  - Description: Review Stage 1 against roadmap criteria after implementation tasks are validated; update Mission Review and Mission State.
  - Owner: Studio Director -> Validator -> Historian
  - Related Mission Milestone: Stage 1 — Technical Foundation
  - Related Roadmap / Review / Backlog Item: Stage 1 readiness criteria
  - Dependencies:
    - MISSION-IDLE-MATH-STAGE-1-T003
    - MISSION-IDLE-MATH-STAGE-1-T004
    - MISSION-IDLE-MATH-STAGE-1-T005
  - Status: Planned
  - Stop Condition Risk: Milestone completion triggers Mission stop and review.

## Execution Order

- Order: 1
  - Task ID: MISSION-IDLE-MATH-STAGE-1-T001
  - Reason: Foundation economy refactor required before tests and UI explanation.
  - Can Run In Parallel With: None
  - Blocks: T003, T004
- Order: 2
  - Task ID: MISSION-IDLE-MATH-STAGE-1-T002
  - Reason: Persistence extraction required before save/load tests.
  - Can Run In Parallel With: None
  - Blocks: T003, T004
- Order: 3
  - Task ID: MISSION-IDLE-MATH-STAGE-1-T003
  - Reason: XCTest target must exist before test coverage can be added.
  - Can Run In Parallel With: None
  - Blocks: T004, T005 validation confidence
- Order: 4
  - Task ID: MISSION-IDLE-MATH-STAGE-1-T004
  - Reason: Base tests are the core testability foundation for Stage 1.
  - Can Run In Parallel With: None
  - Blocks: T005 confidence, T006
- Order: 5
  - Task ID: MISSION-IDLE-MATH-STAGE-1-T005
  - Reason: Gameplay ID centralization is safer after tests exist.
  - Can Run In Parallel With: None
  - Blocks: T006
- Order: 6
  - Task ID: MISSION-IDLE-MATH-STAGE-1-T006
  - Reason: Mission must stop and review after Stage 1 completion.
  - Can Run In Parallel With: None
  - Blocks: Mission Complete

## Mission Dependencies

- Dependent Task: T003
  - Dependency Source: T001 and T002
  - Dependency Type: Technical readiness
  - Reason: Tests need pure economy and persistence surfaces to target.
  - Impact On Mission: T003 is the first active task only because T001 and T002 are completed pre-mission work.
- Dependent Task: T004
  - Dependency Source: T003
  - Dependency Type: Test infrastructure
  - Reason: Base coverage requires a working XCTest target.
  - Impact On Mission: Blocks completion of testability foundation.
- Dependent Task: T005
  - Dependency Source: T003/T004
  - Dependency Type: Regression safety
  - Reason: Replacing gameplay ids is safer with tests present.
  - Impact On Mission: Can be planned after test foundation.
- Dependent Task: T006
  - Dependency Source: T003/T004/T005 and validation evidence
  - Dependency Type: Milestone acceptance
  - Reason: Stage 1 completion must be reviewed against roadmap criteria.
  - Impact On Mission: Completion review decides whether Mission stops as completed.

## Scope Protection Check

- Roadmap Boundary: Stage 1 — Technical Foundation only.
- Product Boundary: No new mechanics, no UI/UX scope from Stage 2, no balance redesign.
- Architecture Boundary: Local testability and foundation work only; no broad project rewrite.
- Out Of Scope Work:
  - Proof Preview Pass.
  - Research Section Readability Pass.
  - Dynamic Research Determinism and Generator Tests.
  - Formula Economy Explanation UI.
  - Stage 2+ roadmap work.
- Potential Opportunities:
  - Add a formal alias or copy of `IDLE_MATH_LAB_REVIEW_AND_ROADMAP.md` if trace naming remains confusing.
  - Add a future mission for Stage 2 after Stage 1 completion.

## Next Backlog Item

- Task ID: MISSION-IDLE-MATH-STAGE-1-T003
- Title: Add XCTest Target for Pure Logic
- Status: Ready
- Reason: Roadmap explicitly places test target after EconomySnapshot and GameSaveStore; current project has no `Idle Math LabTests` folder or test files.

## Single-Step Loop Readiness

- Selected Backlog Item: MISSION-IDLE-MATH-STAGE-1-T003
- Selection Source: Startup Mission Review and Mission Backlog execution order.
- Budget Check: Passed
- Stop Condition Check: Passed
- Source Of Work Check: Passed
- Trace Check: Passed
- Execution Status: Not Started
- Required Next Role: Delivery Planner
- Required Next Artifact: Task Specification for T003
- Stop Rule: After T003 completes Validation or becomes Blocked, Mission must stop and record a Mission Execution Record before any further backlog item can start.

## Planning Assumptions

- EconomySnapshot/EconomyCalculator and GameSaveStore are treated as already completed because the user explicitly instructed to use them as completed work.
- Completed pre-mission work still requires validation once test infrastructure exists.
- Mission Backlog is not a Task Specification. No implementation should start from this file alone.
