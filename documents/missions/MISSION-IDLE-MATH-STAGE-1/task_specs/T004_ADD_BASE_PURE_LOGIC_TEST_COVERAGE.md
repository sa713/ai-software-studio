# Task Specification: MISSION-IDLE-MATH-STAGE-1-T004 — Add Base Pure Logic Test Coverage

## Metadata

- Project ID: Idle Math Lab
- Backlog Task ID: MISSION-IDLE-MATH-STAGE-1-T004
- Version: v0.1
- Creation Date: 2026-06-22
- Author: Delivery Planner
- Source Artifacts:
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION_STATE.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION_BACKLOG.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/validation_reports/T003_VALIDATION_REPORT.md`
  - `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`

## Source Of Work

- Source: `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION_BACKLOG.md`
- Source Type: Mission Backlog Item
- Source Reference: MISSION-IDLE-MATH-STAGE-1-T004 — Add Base Pure Logic Test Coverage
- Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Idle Math Lab Stage 1 Technical Foundation / Stage 1 readiness criteria / Immediate Implementation Queue item 3 -> Backlog Item: MISSION-IDLE-MATH-STAGE-1-T004 -> Task Specification: Add Base Pure Logic Test Coverage

## Objective

- Objective: Add the first pure-logic XCTest coverage for Stage 1 technical foundation.
- Expected Outcome: The test target created in T003 verifies representative income, Proof reward, offline cap, save fallback, state decoding, theorem allocation and research project readiness behavior without UI-test infrastructure.

## Scope

- In Scope Items:
  - Add XCTest files under `Idle Math LabTests`.
  - Add tests for `EconomyCalculator` income snapshot and Proof reward preview.
  - Add tests for offline progress capping through `GameEngine` using an isolated `GameSaveStore`.
  - Add tests for `GameSaveStore` round-trip and corrupted save fallback.
  - Add tests for `GameState` decoding defaults and normalization.
  - Add tests for `TheoremAllocation` normalization.
  - Add a narrow research project readiness test if it can be covered without UI or product decisions.
  - Update the Xcode project to include the new test files in `Idle Math LabTests`.

## Out Of Scope

- Out Of Scope Items:
  - Changing gameplay balance, formulas, Proof rules, project requirements or save format semantics.
  - Adding UI tests or SwiftUI view tests.
  - Refactoring pure logic into a framework or Swift package.
  - Centralizing gameplay ids.
  - Testing Dynamic Research generator determinism.
- Reason: These are separate roadmap items or require product/architecture decisions outside T004.

## Requirements

- Requirement: Base tests must run through the existing `Idle Math LabTests` target.
  - Source: T003 validation result and Mission Backlog T004 dependency.
  - Notes: Do not create a second test target.
- Requirement: Tests must cover income and Proof reward behavior.
  - Source: Idle Math Lab roadmap Stage 1 readiness criteria.
  - Notes: Use deterministic `GameState` inputs and `EconomyCalculator`.
- Requirement: Tests must cover offline cap behavior.
  - Source: Mission milestone completion criteria.
  - Notes: Use isolated test `UserDefaults` to avoid user save data.
- Requirement: Tests must cover state decoding and save fallback behavior.
  - Source: Mission Backlog T004 and Stage 1 persistence foundation.
  - Notes: Include legacy/missing-field decoding and corrupted save fallback.
- Requirement: Tests must cover theorem allocation behavior.
  - Source: Mission milestone completion criteria.
  - Notes: Verify negative-value protection and max-total normalization.
- Requirement: Tests must remain pure-logic oriented.
  - Source: Mission Backlog T004.
  - Notes: Do not instantiate app UI views or UI-test runners.

## Constraints

- Constraint: Do not change product behavior to make tests pass unless a local implementation defect directly blocks a T004 acceptance criterion.
  - Source: Mission Scope Protection and Implementer rules.
  - Impact: Any behavior ambiguity must be recorded as risk or Opportunity.
- Constraint: Keep test data deterministic and local.
  - Source: Validator test evidence requirements.
  - Impact: Do not depend on existing user saves, wall-clock values beyond bounded offline cap checks, network or UI.
- Constraint: Preserve T005 scope.
  - Source: Mission Backlog split.
  - Impact: Gameplay ID centralization must not be performed in T004.

## Dependencies

- Dependency: MISSION-IDLE-MATH-STAGE-1-T003 — Add XCTest Target for Pure Logic
  - Type: Test infrastructure
  - Source: T003 Validation Report
  - Reason: T004 requires a working XCTest target.
  - Impact: T004 can proceed because T003 passed validation.

## Implementation Notes

- Note: Prefer small focused test files over one broad file.
  - Source: Validator readability and traceability needs.
- Note: Use `UserDefaults(suiteName:)` and a unique state key for persistence tests.
  - Source: Scope Protection and user-data safety.
- Note: If a test exposes a product ambiguity rather than a clear defect, do not encode the disputed behavior as a required assertion.
  - Source: Stop Conditions and Product Owner boundary.

## Acceptance Criteria

- Criterion: `xcodebuild test` succeeds for the `Idle Math Lab` scheme.
  - Verification Method: Run `xcodebuild test -project "Idle Math Lab.xcodeproj" -scheme "Idle Math Lab" -destination "platform=iOS Simulator,name=iPhone 17"`.
  - Source: Idle Math Lab roadmap Stage 1.
- Criterion: Tests cover income snapshot and Proof reward preview.
  - Verification Method: Inspect and run `EconomyCalculatorTests`.
  - Source: Mission milestone completion criteria.
- Criterion: Tests cover offline cap behavior.
  - Verification Method: Inspect and run offline progress tests.
  - Source: Mission milestone completion criteria.
- Criterion: Tests cover save fallback and state decoding defaults.
  - Verification Method: Inspect and run `GameSaveStoreTests` and `GameStateTests`.
  - Source: Mission Backlog T004.
- Criterion: Tests cover theorem allocation normalization.
  - Verification Method: Inspect and run `TheoremAllocationTests`.
  - Source: Mission milestone completion criteria.
- Criterion: Tests stay within pure logic and do not change UI or gameplay scope.
  - Verification Method: Inspect changed files and compare with Task Specification scope.
  - Source: Mission Scope Protection.
