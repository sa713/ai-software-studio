# Implementation Report: MISSION-IDLE-MATH-STAGE-1-T005 — Centralize Gameplay IDs

## Metadata

- Project ID: Idle Math Lab
- Backlog Task ID: MISSION-IDLE-MATH-STAGE-1-T005
- Task Specification: `documents/missions/MISSION-IDLE-MATH-STAGE-1/task_specs/T005_CENTRALIZE_GAMEPLAY_IDS.md`
- Version: v0.1
- Creation Date: 2026-06-22
- Author: Implementer
- Source Artifacts:
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION_BACKLOG.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/task_specs/T005_CENTRALIZE_GAMEPLAY_IDS.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/validation_reports/T004_VALIDATION_REPORT.md`
  - `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`

## Completed Work

- Item: Added `GameIDs.swift`.
  - Related Requirement: Add a central typed id source.
  - Related Acceptance Criteria: Central `GameIDs.swift` exists and is included in the app target.
  - Notes: Constants preserve existing string values for upgrades, formula focuses, scientific paradigms, active functions, research projects and eras.
- Item: Replaced core raw ids with `GameIDs`.
  - Related Requirement: Replace highest-risk duplicated raw strings in core logic.
  - Related Acceptance Criteria: Core gameplay logic and tests use centralized ids.
  - Notes: Updated economy logic, upgrade/focus/paradigm/function/project catalogs, formula/era helpers, notebook unlock checks and tests.
- Item: Preserved behavior with tests.
  - Related Requirement: Preserve existing behavior.
  - Related Acceptance Criteria: Existing gameplay behavior is preserved.
  - Notes: Full XCTest suite passed after centralization.

## Modified Files

- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/GameIDs.swift`
  - Change Type: Added
  - Summary: Added central id constants.
  - Related Requirement: Add a central typed id source.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab.xcodeproj/project.pbxproj`
  - Change Type: Modified
  - Summary: Added `GameIDs.swift` to the app target.
  - Related Requirement: Central id source included in app target.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/EconomyCalculator.swift`
  - Change Type: Modified
  - Summary: Replaced core economy upgrade, focus and paradigm raw ids with constants.
  - Related Requirement: Replace highest-risk duplicated raw strings in core logic.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/Upgrade.swift`
  - Change Type: Modified
  - Summary: Replaced upgrade definition ids with constants.
  - Related Requirement: Centralize upgrade ids.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/FormulaFocusCatalog.swift`
  - Change Type: Modified
  - Summary: Replaced focus ids and strengthened upgrade ids with constants.
  - Related Requirement: Centralize focus ids.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/ScientificParadigmCatalog.swift`
  - Change Type: Modified
  - Summary: Replaced paradigm ids with constants.
  - Related Requirement: Centralize paradigm ids.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/FunctionCatalog.swift`
  - Change Type: Modified
  - Summary: Replaced active function, unlock upgrade and focus ids with constants.
  - Related Requirement: Centralize active function ids.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/ProjectCatalog.swift`
  - Change Type: Modified
  - Summary: Replaced project, upgrade, focus and era ids with constants.
  - Related Requirement: Centralize project ids.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/FormulaBuilder.swift`
  - Change Type: Modified
  - Summary: Replaced formula upgrade id checks with constants.
  - Related Requirement: Replace core raw ids.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/FormulaIdentityBuilder.swift`
  - Change Type: Modified
  - Summary: Replaced focus, paradigm and era id switch cases with constants.
  - Related Requirement: Replace core raw ids.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/EraCatalog.swift`
  - Change Type: Modified
  - Summary: Replaced era ids and unlock upgrade id checks with constants.
  - Related Requirement: Replace core raw ids.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/GameEngine.swift`
  - Change Type: Modified
  - Summary: Replaced computation focus runtime check with constant.
  - Related Requirement: Replace core raw ids.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/NotebookCatalog.swift`
  - Change Type: Modified
  - Summary: Replaced unlock-condition gameplay ids with constants while keeping notebook entry content ids unchanged.
  - Related Requirement: Replace highest-risk duplicated raw strings.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/ResearchAffinity.swift`
  - Change Type: Modified
  - Summary: Replaced focus ids with constants.
  - Related Requirement: Centralize focus ids.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/ResearchProject.swift`
  - Change Type: Modified
  - Summary: Replaced branch focus ids with constants.
  - Related Requirement: Centralize focus ids.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/TheoremAllocation.swift`
  - Change Type: Modified
  - Summary: Replaced theorem school focus ids with constants.
  - Related Requirement: Centralize focus ids.
- File: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math LabTests/*.swift`
  - Change Type: Modified
  - Summary: Replaced direct test state/project ids with constants where they are gameplay ids.
  - Related Requirement: Core tests use centralized ids.

## Tests Added

- Test: Existing `Idle Math LabTests` suite
  - Type: XCTest unit test suite
  - Covers: T004 baseline regression coverage after id centralization.
  - Result: Passed via `xcodebuild test -project "Idle Math Lab.xcodeproj" -scheme "Idle Math Lab" -destination "platform=iOS Simulator,name=iPhone 17"`.

## Acceptance Criteria Status

- Criterion: A central `GameIDs.swift` or equivalent file exists and is included in the app target.
  - Status: Passed
  - Verification Method: Inspect source and Xcode project membership.
  - Evidence: `GameIDs.swift` exists and `project.pbxproj` includes it in Sources.
  - Notes: None.
- Criterion: Core gameplay logic and tests use centralized ids for upgrades, formula focuses, paradigms, active functions and projects.
  - Status: Passed
  - Verification Method: Inspect changed core files and run `rg`.
  - Evidence: Economy, core catalogs, runtime checks and tests use `GameIDs`.
  - Notes: Dynamic Research content-catalog literals remain as scoped Opportunity.
- Criterion: Existing gameplay behavior is preserved.
  - Status: Passed
  - Verification Method: Run `xcodebuild test`.
  - Evidence: `** TEST SUCCEEDED **`.
  - Notes: None.
- Criterion: Remaining id cleanup, if any, is recorded as Opportunity rather than silently expanding scope.
  - Status: Passed
  - Verification Method: Implementation report and validation report.
  - Evidence: Dynamic Research broader catalog cleanup is listed as Opportunity.
  - Notes: None.

## Technical Decisions

- Decision: Use a static namespace `GameIDs`.
  - Reason: Matches the app's lightweight model style and avoids new runtime abstractions.
  - Alternatives Considered: New struct types or enum raw values for every id family.
  - Consequences: Existing string persistence remains unchanged while call sites gain a central source.
  - Related Files:
    - `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/GameIDs.swift`
- Decision: Keep Dynamic Research catalog id cleanup out of T005.
  - Reason: That file mixes generated task content, chain ids and future determinism concerns; broad cleanup risks becoming a content/model refactor.
  - Alternatives Considered: Replace every remaining literal in the project.
  - Consequences: Core Stage 1 criteria are met; remaining cleanup is tracked as Opportunity.
  - Related Files:
    - `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/DynamicResearchCatalog.swift`

## Deviations

- Deviation: None.
  - Reason: Not applicable.
  - Impact: None.
  - Approved By: Not applicable.
  - Follow-Up: None.

## Technical Debt Found

- Debt: Dynamic Research catalog still contains raw gameplay id literals.
  - Location: `/Users/sa/Documents/codex/ios/Idle Math Lab/Idle Math Lab/DynamicResearchCatalog.swift`
  - Impact: Non-blocking for Stage 1; dynamic research determinism is already a later roadmap item.
  - Consequences: Future changes to dynamic research ids still need care.
  - Recommendation: Treat as an Opportunity for a later Dynamic Research cleanup or determinism task.

## Known Issues

- Issue: None blocking.
  - Impact: None.
  - Workaround: None.
  - Required Follow-Up: Run Stage 1 completion review.
