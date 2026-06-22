# Task Specification: MISSION-IDLE-MATH-STAGE-1-T006 — Stage 1 Completion Review

## Metadata

- Project ID: Idle Math Lab
- Backlog Task ID: MISSION-IDLE-MATH-STAGE-1-T006
- Version: v0.1
- Creation Date: 2026-06-22
- Author: Delivery Planner
- Source Artifacts:
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION_BACKLOG.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/validation_reports/T003_VALIDATION_REPORT.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/validation_reports/T004_VALIDATION_REPORT.md`
  - `documents/missions/MISSION-IDLE-MATH-STAGE-1/validation_reports/T005_VALIDATION_REPORT.md`
  - `/Users/sa/Documents/codex/ios/Idle Math Lab/IDLE_MATH_LAB_ROADMAP.md`

## Source Of Work

- Source: `documents/missions/MISSION-IDLE-MATH-STAGE-1/MISSION_BACKLOG.md`
- Source Type: Mission Backlog Item
- Source Reference: MISSION-IDLE-MATH-STAGE-1-T006 — Stage 1 Completion Review
- Trace: Mission: MISSION-IDLE-MATH-STAGE-1 -> Roadmap: Idle Math Lab Stage 1 Technical Foundation / Stage 1 completion criteria -> Backlog Item: MISSION-IDLE-MATH-STAGE-1-T006 -> Task Specification: Stage 1 Completion Review

## Objective

- Objective: Review Stage 1 Technical Foundation against roadmap and Mission completion criteria.
- Expected Outcome: Studio Director has enough evidence to mark Stage 1 complete or identify required rework and stop the Mission Run.

## Scope

- In Scope Items:
  - Check Stage 1 criteria from roadmap and Mission milestone.
  - Review validation results for T003, T004 and T005.
  - Confirm stop conditions and autonomy budget state.
  - Update Mission State, Mission Backlog and Mission Review.

## Out Of Scope

- Out Of Scope Items:
  - New implementation work.
  - Stage 2 planning or implementation.
  - Product decisions or roadmap changes.
- Reason: T006 is a review task and milestone stop point.

## Requirements

- Requirement: Stage 1 criteria must be checked with evidence.
  - Source: Mission milestone and Idle Math Lab roadmap.
  - Notes: Use code inspection and test results.
- Requirement: Mission must stop if milestone is complete.
  - Source: Mission Stop Conditions.
  - Notes: Stop reason should be milestone completion.

## Constraints

- Constraint: Do not extend Mission scope.
  - Source: Scope Protection.
  - Impact: Any new idea must become Opportunity.

## Dependencies

- Dependency: T003, T004 and T005 validations.
  - Type: Completion evidence
  - Source: Validation reports.
  - Reason: Stage 1 review depends on implementation task results.
  - Impact: T006 can proceed because all required validation reports exist.

## Implementation Notes

- Note: T006 produces Mission artifact updates, not app code.
  - Source: Mission lifecycle.

## Acceptance Criteria

- Criterion: Mission State records Stage 1 as completed or stopped with reason.
  - Verification Method: Inspect `MISSION_STATE.md`.
  - Source: Mission lifecycle.
- Criterion: Mission Review contains execution records and final stop reason.
  - Verification Method: Inspect `MISSION_REVIEW.md`.
  - Source: Mission lifecycle.
- Criterion: Backlog statuses reflect completed Stage 1 items.
  - Verification Method: Inspect `MISSION_BACKLOG.md`.
  - Source: Mission Backlog.
