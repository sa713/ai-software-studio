# Task Specification: MISSION-IDLE-MATH-STAGE-1-T003 — Add XCTest Target for Pure Logic

## Metadata

- Project ID: Idle Math Lab
- Backlog Task ID: MISSION-IDLE-MATH-STAGE-1-T003
- Version: v0.1
- Creation Date: 2026-06-22
- Author: Delivery Planner
- Source Artifacts:
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION_STATE.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION_BACKLOG.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION_REVIEW.md`
  - `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`

## Source Of Work

- Source: `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION_BACKLOG.md`
- Source Type: Mission Backlog Item
- Source Reference: MISSION-IDLE-MATH-STAGE-1-T003 — Add XCTest Target for Pure Logic
- Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Idle Math Lab Stage 1 Technical Foundation / Immediate Implementation Queue item 3 -> Backlog Item: MISSION-IDLE-MATH-STAGE-1-T003 -> Task Specification: Add XCTest Target for Pure Logic

## Objective

- Objective: Add a buildable XCTest unit-test target for Idle Math Lab pure logic.
- Expected Outcome: The Xcode project contains an `Idle Math LabTests` unit-test target and at least one smoke test that can run without UI test infrastructure, proving the test target is available for T004 base pure-logic coverage.

## Scope

- In Scope Items:
  - Add an `Idle Math LabTests` XCTest unit-test target to `Idle Math Lab.xcodeproj/project.pbxproj`.
  - Add a test source folder `Idle Math LabTests`.
  - Add a minimal test file that imports the app module with `@testable import IdleMathLab` and verifies a pure logic object is reachable.
  - Add or update scheme metadata only if required for `xcodebuild test` discovery.
  - Preserve the existing app target behavior and app source membership.

## Out Of Scope

- Out Of Scope Items:
  - Full income, Proof reward, offline cap, state decoding, theorem allocation or research progress test coverage.
  - Changing gameplay formulas, balance constants, save format semantics, UI, app navigation or product behavior.
  - Centralizing gameplay ids.
  - Refactoring app logic into a new framework or package.
- Reason: These are separate Stage 1 backlog items or later roadmap work. T003 exists only to establish test infrastructure.

## Requirements

- Requirement: The project must expose a unit-test target named `Idle Math LabTests`.
  - Source: Idle Math Lab roadmap Stage 1 and Mission Backlog T003.
  - Notes: The target must be an XCTest unit-test target, not a UI-test target.
- Requirement: The test target must be discoverable by `xcodebuild test`.
  - Source: Idle Math Lab roadmap Immediate Implementation Queue item 3.
  - Notes: A shared scheme may be added if the project does not otherwise expose the test target to the CLI.
- Requirement: The initial test must be pure-logic oriented.
  - Source: Mission Backlog T003.
  - Notes: The smoke test may use `GameState.fresh` or an equivalent model-level object, but must not instantiate SwiftUI views or UI test infrastructure.
- Requirement: The task must preserve T004 as the owner of substantive test coverage.
  - Source: Mission Backlog split between T003 and T004.
  - Notes: Do not add the full Stage 1 test suite in T003.

## Constraints

- Constraint: Do not change Idle Math Lab vision, roadmap, mechanics or balance.
  - Source: Mission Scope Protection.
  - Impact: Any formula or behavior ambiguity must be recorded as risk or Opportunity, not resolved in this task.
- Constraint: Do not expand Stage 1.
  - Source: Mission Boundaries.
  - Impact: Only files needed for XCTest target setup may be changed.
- Constraint: Work with the existing Xcode project.
  - Source: Current project structure.
  - Impact: Avoid introducing new package managers, build systems or framework targets.
- Constraint: Preserve traceability.
  - Source: Mission Mode rules in Delivery Planner and Validator instructions.
  - Impact: Implementation and validation reports must reference this Task Specification and Mission Backlog item.

## Dependencies

- Dependency: MISSION-IDLE-MATH-STAGE-1-T001 — EconomySnapshot and Income Breakdown
  - Type: Technical readiness
  - Source: Mission Backlog
  - Reason: Pure-logic tests need stable logic surfaces.
  - Impact: Treated as completed pre-mission context.
- Dependency: MISSION-IDLE-MATH-STAGE-1-T002 — GameSaveStore with Versioned Save
  - Type: Technical readiness
  - Source: Mission Backlog
  - Reason: Later save/load tests need persistence separated from `GameEngine`.
  - Impact: Treated as completed pre-mission context.

## Implementation Notes

- Note: Prefer the smallest Xcode project change that creates a normal XCTest unit-test bundle.
  - Source: Scope Protection and current project structure.
- Note: If `xcodebuild test` cannot run because the local simulator service is unavailable, record the environment limitation separately from project validity.
  - Source: Validator rules for test execution limitations.
- Note: Use `IdleMathLab` as the app module name if importing the app target from tests.
  - Source: Existing app target build setting `PRODUCT_MODULE_NAME = IdleMathLab`.

## Acceptance Criteria

- Criterion: `Idle Math Lab.xcodeproj/project.pbxproj` contains an `Idle Math LabTests` XCTest unit-test target.
  - Verification Method: Inspect the project file and/or run `xcodebuild -list -project "Idle Math Lab.xcodeproj"`.
  - Source: Mission Backlog T003.
- Criterion: `Idle Math LabTests` contains at least one XCTest source file for pure logic smoke coverage.
  - Verification Method: Inspect `Idle Math LabTests/*.swift`.
  - Source: Mission Backlog T003.
- Criterion: The test target does not introduce UI-test infrastructure or product behavior changes.
  - Verification Method: Inspect changed files and confirm no UI-test target, gameplay logic changes or roadmap changes were made.
  - Source: Mission Scope Protection.
- Criterion: The new target is ready for T004 base pure-logic test coverage.
  - Verification Method: Run or attempt `xcodebuild test`; if blocked by environment, document the blocker and confirm target/scheme structure is present.
  - Source: Mission Backlog T003 and Idle Math Lab roadmap Stage 1.
