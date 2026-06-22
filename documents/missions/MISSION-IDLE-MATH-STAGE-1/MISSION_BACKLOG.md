# MISSION_BACKLOG.md
v0.3
2026-06-22

## Metadata

- Project ID: Idle Math Lab
- Mission ID: MISSION-IDLE-MATH-STAGE-1
- Version: v0.3
- Creation Date: 2026-06-22
- Last Updated: 2026-06-22
- Author: Delivery Planner
- Source Artifacts:
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION.md`
  - `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
  - `ideas/roadmap_v03_mission_mode.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION_RETROSPECTIVE.md`
- Mission Definition: `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION.md`

## Mission Work Summary

- Mission Goal: Завершить Stage 1 — Technical Foundation из Idle Math Lab roadmap.
- Mission Run Autonomy Level: Bounded Multi-Cycle Mission
- Execution Strategy: Use pre-mission T001/T002 foundation, then run Mission Loop for test target, base pure-logic coverage, gameplay id centralization and completion review.
- Classification Note: The actual pilot run completed multiple implementation cycles in one bounded Mission Run; the Single-Step mismatch is recorded in `MISSION_RETROSPECTIVE.md`.
- Key Dependencies:
  - T003 depended on T001/T002.
  - T004 depended on a working XCTest target from T003.
  - T005 depended on T004 regression safety.
  - T006 depended on T003/T004/T005 validation evidence.
- Known Risks:
  - Dynamic Research catalog raw ids remain as a future cleanup Opportunity.
  - Idle Math Lab working tree had pre-mission uncommitted changes before this run.

## Mission Tasks

- Task ID: MISSION-IDLE-MATH-STAGE-1-T001
  - Title: EconomySnapshot and Income Breakdown
  - Source Of Work:
    - Source: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
    - Source Type: Roadmap
    - Source Reference: Stage 1 Technical Foundation; Immediate Implementation Queue item 1
    - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Idle Math Lab Stage 1 Technical Foundation -> Backlog Item: EconomySnapshot and Income Breakdown
  - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Stage 1 Technical Foundation -> Backlog Item: MISSION-IDLE-MATH-STAGE-1-T001
  - Description: Extract economy calculation from `GameEngine.swift` into `EconomyCalculator` and return `EconomySnapshot`.
  - Owner: Implementer
  - Related Mission Milestone: Stage 1 — Technical Foundation
  - Related Roadmap / Review / Backlog Item: `EconomySnapshot and Income Breakdown`
  - Dependencies: None
  - Status: Done
  - Status Notes: Completed before Mission Framework creation; covered by T004 tests.
  - Stop Condition Risk: None

- Task ID: MISSION-IDLE-MATH-STAGE-1-T002
  - Title: GameSaveStore with Versioned Save
  - Source Of Work:
    - Source: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
    - Source Type: Roadmap
    - Source Reference: Stage 1 Technical Foundation; Immediate Implementation Queue item 2
    - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Idle Math Lab Stage 1 Technical Foundation -> Backlog Item: GameSaveStore with Versioned Save
  - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Stage 1 Technical Foundation -> Backlog Item: MISSION-IDLE-MATH-STAGE-1-T002
  - Description: Extract save/load/reset from `GameEngine` into `GameSaveStore` and preserve legacy save behavior.
  - Owner: Implementer
  - Related Mission Milestone: Stage 1 — Technical Foundation
  - Related Roadmap / Review / Backlog Item: `GameSaveStore with Versioned Save`
  - Dependencies: T001
  - Status: Done
  - Status Notes: Completed before Mission Framework creation; covered by T004 tests.
  - Stop Condition Risk: None

- Task ID: MISSION-IDLE-MATH-STAGE-1-T003
  - Title: Add XCTest Target for Pure Logic
  - Source Of Work:
    - Source: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
    - Source Type: Roadmap
    - Source Reference: Stage 1 Technical Foundation; Immediate Implementation Queue item 3
    - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Idle Math Lab Stage 1 Technical Foundation -> Backlog Item: Add XCTest Target for Pure Logic
  - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Stage 1 Technical Foundation -> Backlog Item: MISSION-IDLE-MATH-STAGE-1-T003
  - Description: Add an iOS XCTest target for pure logic.
  - Owner: Delivery Planner -> Implementer -> Validator
  - Related Mission Milestone: Stage 1 — Technical Foundation
  - Related Roadmap / Review / Backlog Item: `Add XCTest Target for Pure Logic`
  - Dependencies: T001, T002
  - Status: Done
  - Status Notes: Task Spec, Implementation Report and Validation Report created; `xcodebuild test` passed.
  - Stop Condition Risk: Resolved; no architecture blocker found.

- Task ID: MISSION-IDLE-MATH-STAGE-1-T004
  - Title: Add Base Pure Logic Test Coverage
  - Source Of Work:
    - Source: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
    - Source Type: Roadmap
    - Source Reference: Stage 1 criteria: income, Proof reward, offline cap, state decoding and theorem allocation tests
    - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Idle Math Lab Stage 1 Technical Foundation -> Backlog Item: Base pure logic tests
  - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Stage 1 Technical Foundation -> Backlog Item: MISSION-IDLE-MATH-STAGE-1-T004
  - Description: Add first tests for economy, Proof reward, offline cap, save fallback, state decoding, theorem allocation and project readiness.
  - Owner: Delivery Planner -> Implementer -> Validator
  - Related Mission Milestone: Stage 1 — Technical Foundation
  - Related Roadmap / Review / Backlog Item: Stage 1 readiness criteria and Immediate Implementation Queue item 3
  - Dependencies: T003
  - Status: Done
  - Status Notes: 11 XCTest cases passed.
  - Stop Condition Risk: Resolved; no product ambiguity blocked tests.

- Task ID: MISSION-IDLE-MATH-STAGE-1-T005
  - Title: Centralize Gameplay IDs
  - Source Of Work:
    - Source: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
    - Source Type: Roadmap
    - Source Reference: Stage 1 Technical Foundation; Immediate Implementation Queue item 6
    - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Idle Math Lab Stage 1 Technical Foundation -> Backlog Item: Centralize Gameplay IDs
  - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Stage 1 Technical Foundation -> Backlog Item: MISSION-IDLE-MATH-STAGE-1-T005
  - Description: Add constants for key upgrade/focus/paradigm/function/project identifiers and replace highest-risk duplicated string literals.
  - Owner: Delivery Planner -> Implementer -> Validator
  - Related Mission Milestone: Stage 1 — Technical Foundation
  - Related Roadmap / Review / Backlog Item: `Centralize Gameplay IDs`
  - Dependencies: T003, T004
  - Status: Done
  - Status Notes: `GameIDs.swift` added; core gameplay logic and tests use centralized ids; Dynamic Research full cleanup remains Opportunity.
  - Stop Condition Risk: Scope risk controlled.

- Task ID: MISSION-IDLE-MATH-STAGE-1-T006
  - Title: Stage 1 Completion Review
  - Source Of Work:
    - Source: `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`
    - Source Type: Roadmap
    - Source Reference: Stage 1 completion criteria
    - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Idle Math Lab Stage 1 Technical Foundation -> Backlog Item: Stage 1 completion criteria
  - Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Stage 1 Technical Foundation -> Backlog Item: MISSION-IDLE-MATH-STAGE-1-T006
  - Description: Review Stage 1 against roadmap criteria after implementation tasks are validated.
  - Owner: Studio Director -> Validator -> Historian
  - Related Mission Milestone: Stage 1 — Technical Foundation
  - Related Roadmap / Review / Backlog Item: Stage 1 readiness criteria
  - Dependencies: T003, T004, T005
  - Status: Done
  - Status Notes: Stage 1 milestone completed; Mission stopped.
  - Stop Condition Risk: Milestone completion triggered Mission stop.

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
  - Blocks: T004
- Order: 4
  - Task ID: MISSION-IDLE-MATH-STAGE-1-T004
  - Reason: Base tests are the core testability foundation for Stage 1.
  - Can Run In Parallel With: None
  - Blocks: T005, T006
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

## Scope Protection Check

- Roadmap Boundary: Stage 1 — Technical Foundation only.
- Product Boundary: No new mechanics, no UI/UX scope from Stage 2, no balance redesign.
- Architecture Boundary: Local testability and foundation work only; no broad project rewrite.
- Out Of Scope Work:
  - Stage 2 Readability and UX.
  - Proof Preview Pass.
  - Research Section Readability Pass.
  - Dynamic Research Determinism and Generator Tests.
  - Formula Economy Explanation UI.
- Potential Opportunities:
  - Future Stage 2 Mission after Product Owner / Studio Director decision.
  - Future Dynamic Research id cleanup and determinism tests.
  - Future hostless pure logic module if test runtime or app-host coupling becomes painful.

## Next Backlog Item

- None. Mission completed.

## Planning Assumptions

- T001 and T002 remain pre-mission context, now covered by T004 tests.
- Dynamic Research full cleanup is not required for Stage 1 completion.
