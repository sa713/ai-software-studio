# ARTIFACTS_ALIGNMENT_REPORT.md
v0.1
2026-06-19

## Назначение

Данный отчёт фиксирует выравнивание `ARTIFACTS.md` с фактической моделью артефактов, описанной в инструкциях агентов AI Software Studio.

Проверены:

- `documents/ARTIFACTS.md`
- `documents/agents/PRODUCT_ANALYST.md`
- `documents/agents/PRODUCT_OWNER.md`
- `documents/agents/SOLUTION_ARCHITECT.md`
- `documents/agents/DELIVERY_PLANNER.md`
- `documents/agents/IMPLEMENTER.md`
- `documents/agents/VALIDATOR.md`
- `documents/agents/HISTORIAN.md`
- `documents/agents/RELEASE_MANAGER.md`

Инструкции агентов не изменялись.

---

# Найденные расхождения

## 1. Metadata не был единообразно определён

В `ARTIFACTS.md` Metadata был явно указан только для Idea Brief, а в инструкциях агентов Metadata существовал почти у всех артефактов.

Изменение:

- добавлено общее правило Metadata;
- для каждого артефакта зафиксированы обязательные поля Metadata;
- для Release Package и Project Memory сохранены специальные поля, соответствующие их фактической модели.

## 2. Discovery Report был описан кратко

`ARTIFACTS.md` содержал основные разделы Discovery Report, но не фиксировал обязательные поля внутри них.

Изменение:

- зафиксированы обязательные поля для Problem Statement, Target Users, Success Criteria, Constraints, Assumptions, Risks и Open Questions;
- добавлено правило, что Discovery Report не должен содержать PRD, архитектуру, Backlog или техническое решение.

## 3. PRD не содержал детальной структуры требований

В `ARTIFACTS.md` были перечислены разделы PRD, но не были определены поля требований, сценариев и критериев приёмки.

Изменение:

- добавлены обязательные поля `ID`, `Requirement`, `Rationale`, `Source`, `Acceptance Link` для функциональных и нефункциональных требований;
- добавлены обязательные поля для User Scenarios, Acceptance Criteria и Out Of Scope;
- зафиксированы допустимые дополнительные разделы PRD.

## 4. Architecture Document не содержал формат ключевых технических разделов

В `ARTIFACTS.md` были перечислены Components, Technology Stack, Data Model, Architectural Decisions, Risks и Constraints, но без обязательных полей.

Изменение:

- добавлены обязательные поля для компонентов, технологий, зависимостей, модели данных, архитектурных решений, рисков и ограничений;
- зафиксирован формат архитектурных решений;
- добавлены допустимые дополнительные разделы Architecture Document.

## 5. Backlog был значительно беднее фактической модели Delivery Planner

`ARTIFACTS.md` описывал Backlog как список задач, но не содержал Execution Order, Dependency Map, Coverage Map и Planning Assumptions.

Изменение:

- добавлены Overview, Execution Order, Tasks, Dependency Map, Coverage Map и Planning Assumptions;
- зафиксированы обязательные поля задач и зависимостей;
- зафиксированы допустимые статусы задач.

## 6. Task Specification не содержал Out Of Scope и Implementation Notes

`ARTIFACTS.md` описывал базовые разделы Task Specification, но не включал фактическую структуру из Delivery Planner.

Изменение:

- добавлены Out Of Scope и Implementation Notes;
- уточнены обязательные поля Objective, Scope, Requirements, Constraints, Dependencies и Acceptance Criteria;
- добавлены допустимые дополнительные разделы.

## 7. Implementation Report не содержал обязательные секции Implementer

`ARTIFACTS.md` содержал Completed Work, Modified Files, Technical Decisions, Deviations и Known Issues, но не содержал Tests Added, Acceptance Criteria Status, Technical Debt Found, Documentation Updated и Self-Check.

Изменение:

- все секции из фактической структуры Implementation Report добавлены в `ARTIFACTS.md`;
- Tests Added, Acceptance Criteria Status, Technical Debt Found, Documentation Updated и Self-Check признаны обязательными разделами;
- для разделов без данных зафиксировано использование `None` или объяснения причины.

## 8. Validation Report имел самое большое расхождение

`ARTIFACTS.md` содержал только Executed Checks, Findings, Risk Assessment и Validation Status.

Инструкция Validator фактически требовала гораздо более полную структуру.

Изменение:

- каноническими обязательными разделами признаны Executed Checks, Scope Validation, Acceptance Criteria Validation, Architecture Validation, Test Validation, Findings, Defect List, Deviations, Risk Assessment, Recommendations, Validation Status, Status Rationale и Required Follow-Up;
- добавлены обязательные поля для каждого раздела;
- зафиксированы допустимые значения Acceptance Criteria status, defect severity и Validation Status.

## 9. Release Package не содержал полную релизную структуру

`ARTIFACTS.md` не содержал Release Scope, Validation Summary, Known Risks и Related Artifacts.

Изменение:

- Release Scope, Validation Summary, Known Risks и Related Artifacts добавлены в каноническую структуру Release Package;
- Known Risks признан обязательным разделом с `None`, если рисков нет;
- Related Artifacts признан обязательным для трассируемости релиза.

## 10. Project Memory не содержал структуру записей

`ARTIFACTS.md` перечислял разделы Project Memory, но не определял поля записей.

Изменение:

- добавлены обязательные поля для Decisions, Decision Rationale, Rejected Alternatives, Technical Debt, Lessons Learned и Future Ideas;
- Active Constraints, Known Risks, Context Notes и Superseded Decisions признаны допустимыми дополнительными разделами;
- Active Constraints, Known Risks и Superseded Decisions отмечены как условно обязательные при наличии соответствующих данных.

---

# Внесённые изменения

`ARTIFACTS.md` обновлён как канонический справочник структур артефактов.

Для каждого артефакта теперь зафиксированы:

- назначение;
- этап создания;
- владелец;
- область, для которой артефакт является источником истины;
- каноническая структура;
- обязательные поля;
- допустимые дополнительные разделы;
- ограничения на недопустимое содержимое.

Список артефактов не изменён.

Жизненный цикл не изменён.

Список ролей не изменён.

Философия Студии не изменена.

---

# Принятые решения

## 1. ARTIFACTS.md является главным источником структуры

Если агентская инструкция содержит пример структуры, он считается рабочей подсказкой, но не заменяет `ARTIFACTS.md`.

## 2. Metadata обязателен для всех артефактов

Общая модель Metadata закреплена в правилах.

Для артефактов со специальной природой применяются уточнения:

- Idea Brief содержит `Source Input`;
- Implementation Report содержит `Backlog Task ID` и `Task Specification`;
- Validation Report содержит `Validation Scope`, `Backlog Task ID`, `Task Specification` и `Implementation Report`;
- Release Package содержит `Version`, `Date`, `Owner` и `Source Artifacts`;
- Project Memory содержит `Last Updated` и `Owner`.

## 3. Validation Report расширен до полной проверочной модели

Все секции, необходимые Validator для независимой проверки, признаны каноническими обязательными.

Это устраняет ситуацию, при которой фактическая структура Validation Report существовала только в инструкции Validator.

## 4. Implementation Report расширен до полной реализационной модели

Tests Added, Acceptance Criteria Status, Technical Debt Found, Documentation Updated и Self-Check признаны обязательными разделами.

Причина: эти разделы нужны для передачи результата Validator и для последующего обновления Project Memory.

## 5. Release Package усилен ради трассируемости

Release Scope, Validation Summary, Known Risks и Related Artifacts включены в каноническую структуру.

Причина: релиз должен показывать не только изменения, но и основание выпуска, проверку, риски и связи с исходными артефактами.

## 6. Project Memory сохраняет компактность

Active Constraints, Known Risks, Context Notes и Superseded Decisions не стали безусловно обязательными разделами.

Они разрешены как дополнительные или условно обязательные, чтобы Project Memory оставался рабочим инструментом, а не копией всех документов.

---

# Обязательные разделы

## Idea Brief

- Metadata
- Idea Title
- Original Description
- Context
- Customer Comments

## Discovery Report

- Metadata
- Problem Statement
- Target Users
- Success Criteria
- Constraints
- Assumptions
- Risks
- Open Questions

## PRD

- Metadata
- Product Goal
- Business Value
- Functional Requirements
- Non-Functional Requirements
- User Scenarios
- Acceptance Criteria
- Out Of Scope

## Architecture Document

- Metadata
- Architecture Overview
- Components
- Technology Stack
- External Dependencies
- Data Model
- Architectural Decisions
- Risks
- Constraints

## Backlog

- Metadata
- Overview
- Execution Order
- Tasks
- Dependency Map
- Coverage Map
- Planning Assumptions

## Task Specification

- Metadata
- Objective
- Scope
- Out Of Scope
- Requirements
- Constraints
- Dependencies
- Implementation Notes
- Acceptance Criteria

## Implementation Report

- Metadata
- Completed Work
- Modified Files
- Tests Added
- Acceptance Criteria Status
- Technical Decisions
- Deviations
- Technical Debt Found
- Known Issues
- Documentation Updated
- Self-Check

## Validation Report

- Metadata
- Executed Checks
- Scope Validation
- Acceptance Criteria Validation
- Architecture Validation
- Test Validation
- Findings
- Defect List
- Deviations
- Risk Assessment
- Recommendations
- Validation Status
- Status Rationale
- Required Follow-Up

## Release Package

- Metadata
- Release Scope
- Features
- Bug Fixes
- Validation Summary
- Known Limitations
- Known Risks
- Deployment Instructions
- Release Notes
- Related Artifacts

## Project Memory

- Metadata
- Decisions
- Decision Rationale
- Rejected Alternatives
- Technical Debt
- Lessons Learned
- Future Ideas

---

# Дополнительные и условно обязательные разделы

## Idea Brief

- Initial Assumptions
- Initial Open Questions
- Related Existing Projects
- Initial Success Signal

## Discovery Report

- Discovery Sources
- Rejected Questions
- Out Of Discovery Scope

## PRD

- Product Assumptions
- Product Risks
- Dependencies
- Open Product Questions
- Glossary

## Architecture Document

- Requirements Coverage
- System Context
- Integration Flows
- Security Considerations
- Deployment Model
- Observability
- Performance Considerations
- Scalability Considerations
- Operational Considerations
- Technical Assumptions
- Open Technical Questions

## Backlog

- Milestones
- Parallelization Notes
- Blocked Items
- Planning Risks

## Task Specification

- Related Components
- Related User Scenarios
- Data Requirements
- Integration Requirements
- Risk Notes
- Handoff Notes

## Implementation Report

- Build Notes
- Manual Verification
- Environment Notes
- Follow-Up Suggestions

## Validation Report

- Validation Environment
- Manual Test Evidence
- Automated Test Output
- Traceability Notes

## Release Package

- Customer Handoff Notes
- Traceability Matrix
- Open Follow-Up Items
- Operational Notes

## Project Memory

Дополнительные разделы:

- Context Notes

Условно обязательные разделы:

- Active Constraints, если есть активные ограничения;
- Known Risks, если есть риски, важные для будущей работы;
- Superseded Decisions, если решения были заменены.

---

# Дополнительная проверка

## Каждый артефакт имеет владельца

Проверено. Владельцы:

- Idea Brief — Product Owner;
- Discovery Report — Product Analyst;
- PRD — Product Owner;
- Architecture Document — Solution Architect;
- Backlog — Delivery Planner;
- Task Specification — Delivery Planner;
- Implementation Report — Implementer;
- Validation Report — Validator;
- Release Package — Release Manager;
- Project Memory — Historian.

## Каждый артефакт имеет этап создания

Проверено. Этап создания зафиксирован в каждом описании артефакта.

## Каждый артефакт имеет источник истины

Проверено. Для каждого артефакта указан раздел `Является источником истины для`.

## Каждый артефакт имеет определённую структуру

Проверено. Для каждого артефакта добавлена каноническая структура с обязательными разделами и полями.

## Артефакты без владельца

Не обнаружены.

## Владельцы без артефактов

Не обнаружены среди ролей, создающих канонические артефакты.

Studio Director владеет Project State, но Project State является служебным объектом, а не продуктовым артефактом.

## Дублирование структур между артефактами

Критического дублирования не обнаружено.

Общие поля Metadata повторяются намеренно как единое правило.

Пересечения по рискам, решениям и ограничениям разведены по назначению:

- Discovery Report фиксирует ранние продуктовые и бизнес-риски;
- Architecture Document фиксирует технические риски и архитектурные решения;
- Implementation Report фиксирует фактические технические решения и найденный долг;
- Validation Report фиксирует результаты проверки и остаточные риски;
- Release Package фиксирует релизные риски и ограничения;
- Project Memory сохраняет долгосрочно значимые решения, причины и знания.

---

# Итог

`ARTIFACTS.md` приведён в соответствие с фактической моделью артефактов Студии.

Структура каждого канонического артефакта теперь определена в `ARTIFACTS.md`.

Уникальные определения структур, ранее существовавшие только в инструкциях агентов, перенесены в канонический документ.

Нерешённых противоречий после обновления не обнаружено.
