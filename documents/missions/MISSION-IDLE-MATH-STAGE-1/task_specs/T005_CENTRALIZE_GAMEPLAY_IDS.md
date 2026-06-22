# Task Specification: MISSION-IDLE-MATH-STAGE-1-T005 — Centralize Gameplay IDs

## Metadata

- Project ID: Idle Math Lab
- Backlog Task ID: MISSION-IDLE-MATH-STAGE-1-T005
- Version: v0.1
- Creation Date: 2026-06-22
- Author: Delivery Planner
- Source Artifacts:
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION_BACKLOG.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/validation_reports/T004_VALIDATION_REPORT.md`
  - `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`

## Source Of Work

- Source: `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION_BACKLOG.md`
- Source Type: Mission Backlog Item
- Source Reference: MISSION-IDLE-MATH-STAGE-1-T005 — Centralize Gameplay IDs
- Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Idle Math Lab Stage 1 Technical Foundation / Immediate Implementation Queue item 6 -> Backlog Item: MISSION-IDLE-MATH-STAGE-1-T005 -> Task Specification: Centralize Gameplay IDs

## Objective

- Objective: Add a typed central source for key gameplay identifiers and replace highest-risk duplicated raw string ids in Stage 1 logic and tests.
- Expected Outcome: `GameIDs.swift` or an equivalent typed source defines upgrade, focus, paradigm, function and project ids used by core gameplay logic; tests pass after replacing core duplicated literals.

## Scope

- In Scope Items:
  - Add `GameIDs.swift` to the app target.
  - Centralize upgrade ids used by economy, catalog definitions, era unlocks, formula building and tests.
  - Centralize formula focus ids used by focus catalog, runtime checks, theorem school mapping, research branch mapping and tests.
  - Centralize scientific paradigm ids used by paradigm catalog and core economy/formula identity checks.
  - Centralize active function ids used by function catalog.
  - Centralize research project ids used by project catalog and tests.
  - Update `Idle Math LabTests` to use centralized ids where tests build states directly.

## Out Of Scope

- Out Of Scope Items:
  - Broad rewrite of all narrative/catalog content in Dynamic Research, Notebook entries or future roadmap systems.
  - Renaming ids or changing save compatibility.
  - Changing gameplay balance, unlock requirements, formulas, project rewards or UI copy.
  - Adding new gameplay ids not present in current Stage 1 scope.
  - Changing tests beyond replacing raw ids with typed constants.
- Reason: T005 is a Stage 1 technical foundation task, not a content model refactor or product redesign.

## Requirements

- Requirement: Add a central typed id source.
  - Source: Idle Math Lab roadmap Stage 1.
  - Notes: The source must preserve existing string values for save compatibility.
- Requirement: Replace highest-risk duplicated raw strings in core logic.
  - Source: Mission Backlog T005.
  - Notes: Prioritize economy calculations, core catalogs, runtime checks and tests.
- Requirement: Preserve existing behavior.
  - Source: Mission Scope Protection.
  - Notes: Existing T004 tests must continue to pass.
- Requirement: Keep future broad cleanup as Opportunity, not implicit scope.
  - Source: Mission Scope Protection.
  - Notes: Any remaining lower-risk raw ids should be recorded rather than forcing a large refactor.

## Constraints

- Constraint: Do not change id string values.
  - Source: Save compatibility and roadmap stability.
  - Impact: All constants must map to the existing persisted ids.
- Constraint: Do not expand into Stage 2 or Dynamic Research generator work.
  - Source: Mission Boundaries.
  - Impact: Dynamic Research determinism and broader catalog refactor remain out of scope.
- Constraint: Stay within file-change budget.
  - Source: Mission Autonomy Budget.
  - Impact: Prefer targeted replacements in core files.

## Dependencies

- Dependency: MISSION-IDLE-MATH-STAGE-1-T004 — Add Base Pure Logic Test Coverage
  - Type: Regression safety
  - Source: T004 Validation Report
  - Reason: Gameplay id centralization is safer with tests in place.
  - Impact: T005 can proceed because T004 passed validation.

## Implementation Notes

- Note: Use nested enums or another lightweight static namespace rather than new runtime model objects.
  - Source: Existing simple Swift app architecture.
- Note: Constants should use existing typealiases where available, such as `UpgradeID`, `FormulaFocusID`, `ScientificParadigmID` and `ActiveFunctionID`.
  - Source: Existing model types.
- Note: After replacement, run the full XCTest suite.
  - Source: Validator requirements and T004 regression coverage.

## Acceptance Criteria

- Criterion: A central `GameIDs.swift` or equivalent file exists and is included in the app target.
  - Verification Method: Inspect source and Xcode project membership.
  - Source: Idle Math Lab roadmap Stage 1.
- Criterion: Core gameplay logic and tests use centralized ids for upgrades, formula focuses, paradigms, active functions and projects.
  - Verification Method: Inspect changed core files and run targeted `rg` checks.
  - Source: Mission Backlog T005.
- Criterion: Existing gameplay behavior is preserved.
  - Verification Method: Run `xcodebuild test`.
  - Source: T004 validation baseline.
- Criterion: Remaining id cleanup, if any, is recorded as Opportunity rather than silently expanding scope.
  - Verification Method: Inspect Validation Report and Mission Review.
  - Source: Mission Scope Protection.
