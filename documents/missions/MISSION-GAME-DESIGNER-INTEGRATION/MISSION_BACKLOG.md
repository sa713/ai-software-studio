# MISSION_BACKLOG.md
v0.1
2026-06-23

## Metadata

- Project ID: AI Software Studio
- Mission ID: MISSION-GAME-DESIGNER-INTEGRATION
- Version: v0.1
- Creation Date: 2026-06-23
- Last Updated: 2026-06-23
- Author: Delivery Planner
- Source Artifacts:
  - `documents/missions/MISSION-GAME-DESIGNER-INTEGRATION/MISSION.md`
  - `ideas/roadmap_game.md`
- Mission Definition: `documents/missions/MISSION-GAME-DESIGNER-INTEGRATION/MISSION.md`

## Mission Work Summary

- Mission Goal: Fully integrate Game Designer into AI Software Studio.
- Mission Run Autonomy Level: Bounded Multi-Cycle Mission
- Execution Strategy: Execute roadmap stages as documentation tasks, validate each stage by artifact presence and traceability checks, then prepare final Game Designer Integration Review.
- Key Dependencies:
  - T001 defines role boundaries before lifecycle integration.
  - T002 depends on T001 because lifecycle needs a role owner.
  - T003 depends on T001 and T002 because artifacts need a lifecycle place and owner.
  - T004 depends on T003 because Game Design Review needs artifact structure.
  - T005 depends on T004 because Gameplay Findings come from Game Design Review.
  - T006 depends on T004 because specialized reviews are subtypes of Game Design Review.
  - T007 depends on T004, T005 and T006 because Mission Mode must preserve review and source-of-work boundaries.
  - T008 depends on all prior tasks.

## Mission Tasks

- Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T001
  - Title: Define Game Designer Responsibility Boundary
  - Source Of Work:
    - Source: `ideas/roadmap_game.md`
    - Source Type: Roadmap
    - Source Reference: Stage 1. Определение зоны ответственности
    - Trace: Mission: MISSION-GAME-DESIGNER-INTEGRATION -> Game Designer Roadmap Stage 1 -> Backlog Item T001
  - Description: Add Game Designer as a canonical role with clear ownership and exclusions.
  - Owner: Studio Director -> Implementer -> Validator
  - Status: Done
  - Status Notes: `AGENTS.md`, `GAME_DESIGNER.md`, `DECISION_AUTHORITY.md`, `PROJECT_STATE.md` updated.

- Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T002
  - Title: Integrate Game Designer Into Production Cycle
  - Source Of Work:
    - Source: `ideas/roadmap_game.md`
    - Source Type: Roadmap
    - Source Reference: Stage 2. Встраивание в производственный цикл
    - Trace: Mission: MISSION-GAME-DESIGNER-INTEGRATION -> Game Designer Roadmap Stage 2 -> Backlog Item T002
  - Description: Document Product Analyst -> UX Designer -> Product Owner -> Game Designer -> Solution Architect -> Delivery Planner handoff for game projects.
  - Owner: Studio Director -> Implementer -> Validator
  - Status: Done
  - Status Notes: `LIFECYCLE.md`, Product Owner, Game Designer, Solution Architect, Delivery Planner and Studio Director docs updated.

- Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T003
  - Title: Define Game Design Artifacts
  - Source Of Work:
    - Source: `ideas/roadmap_game.md`
    - Source Type: Roadmap
    - Source Reference: Stage 3. Game Design Artifacts
    - Trace: Mission: MISSION-GAME-DESIGNER-INTEGRATION -> Game Designer Roadmap Stage 3 -> Backlog Item T003
  - Description: Add canonical definitions for Game Design Notes, Gameplay Risks, Gameplay Opportunities and Game Design Review.
  - Owner: Studio Director -> Implementer -> Validator
  - Status: Done
  - Status Notes: `ARTIFACTS.md` defines `GAME_DESIGN_NOTES.md`, `GAMEPLAY_RISKS.md`, `GAMEPLAY_OPPORTUNITIES.md`, `GAME_DESIGN_REVIEW.md`.

- Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T004
  - Title: Add Game Design Review Mode
  - Source Of Work:
    - Source: `ideas/roadmap_game.md`
    - Source Type: Roadmap
    - Source Reference: Stage 4. Game Design Review Mode
    - Trace: Mission: MISSION-GAME-DESIGNER-INTEGRATION -> Game Designer Roadmap Stage 4 -> Backlog Item T004
  - Description: Define Game Design Review inputs, outputs, severity and recommendations.
  - Owner: Studio Director -> Implementer -> Validator
  - Status: Done
  - Status Notes: `GAME_DESIGNER.md`, `LIFECYCLE.md` and `ARTIFACTS.md` define Game Design Review Mode.

- Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T005
  - Title: Add Gameplay Finding Source Of Work
  - Source Of Work:
    - Source: `ideas/roadmap_game.md`
    - Source Type: Roadmap
    - Source Reference: Stage 5. Gameplay Findings
    - Trace: Mission: MISSION-GAME-DESIGNER-INTEGRATION -> Game Designer Roadmap Stage 5 -> Backlog Item T005
  - Description: Permit Gameplay Finding as Source Of Work only after Product Owner Review.
  - Owner: Studio Director -> Implementer -> Validator
  - Status: Done
  - Status Notes: Source Of Work rules updated in `ARTIFACTS.md`, `DELIVERY_PLANNER.md`, `CODEX_TASK_FORMULATION_PROCESS.md` and role docs.

- Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T006
  - Title: Add Specialized Game Design Reviews
  - Source Of Work:
    - Source: `ideas/roadmap_game.md`
    - Source Type: Roadmap
    - Source Reference: Stage 6. Specialized Reviews
    - Trace: Mission: MISSION-GAME-DESIGNER-INTEGRATION -> Game Designer Roadmap Stage 6 -> Backlog Item T006
  - Description: Define Core Loop Review, Progression Review, Reward Review and Retention Review as specialized Game Design Review modes.
  - Owner: Studio Director -> Implementer -> Validator
  - Status: Done
  - Status Notes: Specialized reviews documented in `GAME_DESIGNER.md`, `ARTIFACTS.md`, `LIFECYCLE.md` and `STUDIO_DIRECTOR.md`.

- Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T007
  - Title: Integrate Game Design Review Into Mission Mode
  - Source Of Work:
    - Source: `ideas/roadmap_game.md`
    - Source Type: Roadmap
    - Source Reference: Stage 7. Mission Mode Integration
    - Trace: Mission: MISSION-GAME-DESIGNER-INTEGRATION -> Game Designer Roadmap Stage 7 -> Backlog Item T007
  - Description: Allow Mission Mode to call Game Design Review after roadmap stage, economy change, progression change or product completion.
  - Owner: Studio Director -> Implementer -> Validator
  - Status: Done
  - Status Notes: `LIFECYCLE.md` and `STUDIO_DIRECTOR.md` document the Game Design Review hook without changing Mission Mode v0.2.

- Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T008
  - Title: Prepare Final Game Designer Integration Review
  - Source Of Work:
    - Source: Mission expected result
    - Source Type: Mission Completion Criteria
    - Source Reference: Game Designer Integration Review
    - Trace: Mission: MISSION-GAME-DESIGNER-INTEGRATION -> Completion Criteria -> Backlog Item T008
  - Description: Review the completed integration and confirm whether a future `Провести Game Design Review Idle Math Lab` mission can run through Game Designer.
  - Owner: Studio Director -> Validator
  - Status: Done
  - Status Notes: `GAME_DESIGNER_INTEGRATION_REVIEW.md` created.

## Execution Order

- Order: 1
  - Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T001
  - Reason: Responsibility boundary is prerequisite for all other changes.
  - Can Run In Parallel With: None
  - Blocks: T002, T003, T004, T005, T006, T007
- Order: 2
  - Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T002
  - Reason: Main lifecycle must know where Game Designer participates.
  - Can Run In Parallel With: None
  - Blocks: T003, T007
- Order: 3
  - Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T003
  - Reason: Game Design artifacts need owner and lifecycle placement.
  - Can Run In Parallel With: T004 after initial Game Designer role exists
  - Blocks: T004, T005, T006
- Order: 4
  - Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T004
  - Reason: Game Design Review Mode defines Gameplay Findings.
  - Can Run In Parallel With: None
  - Blocks: T005, T006, T007
- Order: 5
  - Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T005
  - Reason: Source Of Work rules depend on Gameplay Finding definition.
  - Can Run In Parallel With: None
  - Blocks: T007, T008
- Order: 6
  - Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T006
  - Reason: Specialized reviews depend on Game Design Review Mode.
  - Can Run In Parallel With: None
  - Blocks: T007, T008
- Order: 7
  - Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T007
  - Reason: Mission Mode integration depends on review and source-of-work boundaries.
  - Can Run In Parallel With: None
  - Blocks: T008
- Order: 8
  - Task ID: MISSION-GAME-DESIGNER-INTEGRATION-T008
  - Reason: Final review must evaluate all completed stages.
  - Can Run In Parallel With: None
  - Blocks: Mission Complete

## Scope Protection Check

- Roadmap Boundary: Game Designer Roadmap only.
- Product Boundary: No changes to Idle Math Lab or existing products.
- Mission History Boundary: Existing Mission histories remain untouched.
- UX Boundary: UX Designer roadmap and results remain untouched except for existing role boundary references already present in canonical docs.
- Architecture Boundary: No Mission Mode v0.2 redesign; only documented Game Design Review hook.
- Potential Opportunities:
  - Future Game Design Review of Idle Math Lab can be launched as a separate mission.
  - Future UX and Game Design combined reviews must keep separate artifact ownership.

## Next Backlog Item

- None. Mission completed.

## Planning Assumptions

- Documentation-only implementation is sufficient because the Studio is defined by canonical documents.
- The user's launch request provides the Studio-owner authorization required by `STUDIO_IMPROVEMENT_PROCESS.md` for a new role.
