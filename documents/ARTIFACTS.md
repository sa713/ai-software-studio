# ARTIFACTS.md
v0.1
2026-06-19

## Назначение

Данный документ определяет полный перечень канонических артефактов AI Software Studio и их обязательную структуру.

Артефакт является официальным носителем знаний, решений или результатов работы.

ARTIFACTS.md является единственным источником истины для структуры артефактов. Инструкции агентов могут ссылаться на эти структуры, но не должны быть единственным местом, где структура артефакта определена.

Все взаимодействие между агентами должно происходить через артефакты, Project Memory и процессные решения Studio Director.

Артефакты являются основным способом передачи контекста между этапами жизненного цикла проекта.

---

# Общие правила

## Единственный источник истины

Каждый тип информации должен иметь один канонический артефакт.

Дублирование информации между артефактами запрещено.

Если информация изменилась, обновляется её канонический источник.

Если агентская инструкция содержит пример структуры артефакта, но она расходится с данным документом, действует ARTIFACTS.md.

---

## Владение

Каждый артефакт обязан иметь владельца.

Владелец отвечает за:

- актуальность содержимого;
- качество содержимого;
- своевременное обновление;
- соответствие структуры данному документу.

---

## Версионирование

Каждый артефакт должен иметь версию.

Все изменения должны быть отслеживаемыми.

История изменений должна сохраняться.

---

## Связность

Каждый артефакт обязан содержать ссылки на связанные исходные артефакты или источники.

По артефактам должна восстанавливаться полная история проекта:

```text
Идея
↓
Требования
↓
Архитектура
↓
План
↓
Реализация
↓
Проверка
↓
Релиз
```

---

## Metadata

Если для конкретного артефакта не указано иное, обязательный раздел `Metadata` содержит:

- `Project ID`;
- `Version`;
- `Creation Date`;
- `Author`;
- `Source Artifacts`.

`Source Artifacts` содержит ссылки на артефакты или входы, из которых получен текущий артефакт. Если артефакт создаётся из исходного сообщения заказчика и входных артефактов ещё нет, это должно быть указано явно.

---

## Обязательные и дополнительные разделы

Обязательный раздел должен присутствовать в артефакте всегда.

Если в обязательном разделе нет данных, раздел остаётся в артефакте и содержит `None`, `Not Applicable` или краткое объяснение отсутствия данных.

Условно обязательный раздел должен присутствовать, если применимое знание существует или если условие прямо указано в описании артефакта.

Дополнительный раздел допустим, если он помогает владельцу артефакта зафиксировать важное знание и не дублирует другой канонический артефакт.

Дополнительный раздел не должен заменять обязательные разделы.

---

# Artifact 01. Idea Brief

## Назначение

Фиксация исходной идеи заказчика.

## Этап создания

Stage 1 — Idea

## Владелец

Product Owner

## Является источником истины для

- первоначального замысла проекта;
- исходной формулировки заказчика;
- стартового контекста проекта.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Version`;
- `Creation Date`;
- `Author: Product Owner`;
- `Source Input`;
- `Source Artifacts`.

`Source Input` фиксирует исходное сообщение, описание, файл или другой вход, из которого создан Idea Brief.

### Idea Title

Краткое название идеи.

Обязательные поля:

- `Title`;
- `Reason`, если название сформулировано Студией, а не заказчиком.

### Original Description

Исходное описание идеи заказчиком.

Обязательные поля:

- `Description`;
- `Original Wording Preserved: Yes/No`;
- `Notes`, если описание было нормализовано или сокращено.

### Context

Стартовый контекст, необходимый для Discovery.

Обязательные поля:

- `Known Context`;
- `Known Constraints`;
- `Known Stakeholders`, если они уже известны.

### Customer Comments

Дополнительные комментарии заказчика, которые важно сохранить до Discovery.

Обязательные поля:

- `Comment`;
- `Source`;
- `Date`, если известно.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Initial Assumptions`;
- `Initial Open Questions`;
- `Related Existing Projects`;
- `Initial Success Signal`.

Дополнительные разделы не должны превращать Idea Brief в Discovery Report или PRD.

---

# Artifact 02. Discovery Report

## Назначение

Результат исследования задачи.

## Этап создания

Stage 2 — Discovery

## Владелец

Product Analyst

## Является источником истины для

- понимания проблемы;
- бизнес-контекста;
- пользователей;
- критериев успеха;
- ограничений, допущений, рисков и открытых вопросов, выявленных на Discovery.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Version`;
- `Creation Date`;
- `Author: Product Analyst`;
- `Source Artifacts`.

### Problem Statement

Какую проблему нужно решить и как с ней связано предложенное решение.

Обязательные поля:

- `Problem`;
- `Customer Proposed Solution`, если заказчик предложил решение;
- `Problem-Solution Fit`;
- `Relevant Alternatives`, если очевидные альтернативы важны для риска или бизнес-эффекта.

### Target Users

Для кого создаётся продукт.

Обязательные поля:

- `User Group`;
- `User Goal`;
- `Context of Use`;
- `Priority`, если групп пользователей несколько.

### Success Criteria

Что считается успешным результатом.

Обязательные поля:

- `Criterion`;
- `Measurement or Evidence`;
- `Source`;

### Constraints

Ограничения, влияющие на продукт или реализацию.

Обязательные поля:

- `Constraint`;
- `Type`;
- `Source`;
- `Impact`.

### Assumptions

Допущения, на которых можно продолжать работу.

Обязательные поля:

- `Assumption`;
- `Reason`;
- `Risk`;
- `Validation Need`, если требуется последующая проверка.

### Risks

Риски, которые могут повлиять на достижение цели, качество решения, сроки, возможность реализации или соответствие предложенного решения проблеме.

Обязательные поля:

- `Risk`;
- `Cause`;
- `Impact`;
- `Likelihood or Severity`;
- `Mitigation or Follow-Up`.

### Open Questions

Нерешённые вопросы, влияющие на бизнес-решение, продуктовое решение, архитектурное решение или критерии успеха.

Обязательные поля:

- `Question`;
- `Why It Matters`;
- `Decision Impact`;
- `Owner or Routing`;

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Discovery Sources`;
- `Rejected Questions`;
- `Out Of Discovery Scope`.

Discovery Report не должен содержать PRD, архитектурный дизайн, Backlog или техническое решение.

---

# Artifact 03. Product Requirements Document (PRD)

## Назначение

Главный продуктовый документ проекта.

## Этап создания

Stage 3 — Product Definition

## Владелец

Product Owner

## Является источником истины для

- цели продукта;
- бизнес-ценности;
- состава продукта;
- функциональных требований;
- нефункциональных требований;
- пользовательских сценариев;
- критериев приёмки;
- границ продукта.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Version`;
- `Creation Date`;
- `Author: Product Owner`;
- `Source Artifacts`.

### Product Goal

Цель продукта: какой продукт создаётся, для кого, какую проблему решает и какой результат должен обеспечить.

Обязательные поля:

- `Product`;
- `Target User or Customer`;
- `Problem Solved`;
- `Expected Result`.

### Business Value

Ожидаемая ценность продукта для заказчика, пользователей или бизнеса.

Обязательные поля:

- `Value`;
- `Beneficiary`;
- `Link to Success Criteria`;
- `Rationale`.

### Functional Requirements

Функциональные требования продукта.

Для каждого требования обязательны поля:

- `ID`;
- `Requirement`;
- `Rationale`;
- `Source`;
- `Acceptance Link`.

### Non-Functional Requirements

Требования к качеству продукта.

Для каждого требования обязательны поля:

- `ID`;
- `Requirement`;
- `Rationale`;
- `Source`;
- `Acceptance Link`.

### User Scenarios

Основные пользовательские сценарии.

Для каждого сценария обязательны поля:

- `ID`;
- `User`;
- `Goal`;
- `Preconditions`;
- `Steps`;
- `Expected Result`;
- `Related Requirements`.

### Acceptance Criteria

Критерии приёмки продукта.

Для каждого критерия обязательны поля:

- `ID`;
- `Criterion`;
- `Related Requirements`;
- `Verification Basis`.

### Out Of Scope

Что не входит в продукт.

Для каждого пункта обязательны поля:

- `Item`;
- `Reason`;
- `Impact`.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Product Assumptions`;
- `Product Risks`;
- `Dependencies`;
- `Open Product Questions`;
- `Glossary`.

Дополнительные разделы не должны дублировать Discovery Report и не должны содержать архитектурные решения.

---

# Artifact 04. Architecture Document

## Назначение

Главный технический документ проекта.

## Этап создания

Stage 4 — Solution Design

## Владелец

Solution Architect

## Является источником истины для

- технической архитектуры;
- компонентов системы;
- технологического стека;
- внешних зависимостей;
- модели данных;
- архитектурных решений;
- технических рисков и ограничений.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Version`;
- `Creation Date`;
- `Author: Solution Architect`;
- `Source Artifacts`.

### Architecture Overview

Общее описание архитектуры: тип архитектуры, основные технические идеи, границы системы, ключевые потоки и связь с требованиями PRD.

Обязательные поля:

- `Architecture Type`;
- `System Boundaries`;
- `Key Flows`;
- `Relation to PRD`.

### Components

Основные компоненты системы.

Для каждого компонента обязательны поля:

- `ID`;
- `Name`;
- `Responsibility`;
- `Related Requirements`;
- `Inputs`;
- `Outputs`;
- `Depends On`;
- `External Dependencies`;
- `Notes`.

### Technology Stack

Используемые технологии.

Для каждой существенной технологии обязательны поля:

- `Technology`;
- `Used For`;
- `Reason`;
- `Alternatives Considered`;
- `Consequences`;
- `Risks`;
- `Related Requirements or Constraints`.

### External Dependencies

Внешние зависимости.

Для каждой зависимости обязательны поля:

- `Dependency`;
- `Purpose`;
- `Integration Method`;
- `Criticality`;
- `Reason`;
- `Alternatives`;
- `Risks`;
- `Constraints`.

### Data Model

Основные сущности и данные.

Для каждой сущности обязательны поля:

- `Entity`;
- `Purpose`;
- `Key Fields`;
- `Relationships`;
- `Source of Truth`;
- `Lifecycle`;
- `Privacy or Security Notes`.

### Architectural Decisions

Принятые архитектурные решения.

Для каждого решения обязательны поля:

- `ID`;
- `Decision`;
- `Reason`;
- `Alternatives`;
- `Consequences`;
- `Related Requirements or Constraints`.

### Risks

Технические риски.

Для каждого риска обязательны поля:

- `Risk`;
- `Category`;
- `Cause`;
- `Impact`;
- `Likelihood or Severity`;
- `Mitigation`;
- `Residual Risk`;
- `Related Component, Dependency or Requirement`.

### Constraints

Технические ограничения.

Для каждого ограничения обязательны поля:

- `Constraint`;
- `Source`;
- `Impact`;
- `Architectural Response`.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Requirements Coverage`;
- `System Context`;
- `Integration Flows`;
- `Security Considerations`;
- `Deployment Model`;
- `Observability`;
- `Performance Considerations`;
- `Scalability Considerations`;
- `Operational Considerations`;
- `Technical Assumptions`;
- `Open Technical Questions`.

Дополнительные разделы не должны дублировать PRD, создавать Backlog или превращаться в Task Specifications.

---

# Artifact 05. Backlog

## Назначение

Полный перечень работ проекта.

## Этап создания

Stage 5 — Planning

## Владелец

Delivery Planner

## Является источником истины для

- состава работ проекта;
- порядка реализации;
- зависимостей между задачами;
- связи задач с требованиями PRD и компонентами Architecture Document;
- статуса готовности задач к реализации.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Version`;
- `Creation Date`;
- `Author: Delivery Planner`;
- `Source Artifacts`.

### Overview

Краткое описание состава работ, общего порядка реализации и основных зависимостей.

Обязательные поля:

- `Work Summary`;
- `Execution Strategy`;
- `Key Dependencies`.

### Execution Order

Последовательность выполнения задач.

Для каждого шага обязательны поля:

- `Order`;
- `Task ID`;
- `Reason`;
- `Can Run In Parallel With`;
- `Blocks`.

### Tasks

Полный перечень задач.

Для каждой задачи обязательны поля:

- `ID`;
- `Title`;
- `Description`;
- `Owner`;
- `Related Requirements`;
- `Related Components`;
- `Dependencies`;
- `Priority`;
- `Status`.

Допустимые значения `Status`:

- `Planned`;
- `Ready For Implementation`;
- `Blocked`;
- `In Implementation`;
- `Done`;
- `Removed`.

### Dependency Map

Карта зависимостей между задачами.

Для каждой зависимости обязательны поля:

- `Dependent Task`;
- `Dependency Source`;
- `Dependency Type`;
- `Reason`;
- `Impact On Execution Order`.

### Coverage Map

Покрытие требований и компонентов задачами.

Для каждого требования или компонента обязательны поля:

- `Source`;
- `Covered By Tasks`;
- `Coverage Notes`.

### Planning Assumptions

Допущения, сделанные Delivery Planner без изменения продукта или архитектуры.

Для каждого допущения обязательны поля:

- `Assumption`;
- `Reason`;
- `Risk`;
- `Related Tasks`.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Milestones`;
- `Parallelization Notes`;
- `Blocked Items`;
- `Planning Risks`.

Дополнительные разделы не должны превращать Backlog в PRD, Architecture Document или Implementation Report.

---

# Artifact 06. Task Specification

## Назначение

Контракт на реализацию отдельной задачи.

## Этап создания

Stage 5 — Planning, перед началом реализации задачи.

## Владелец

Delivery Planner

## Является источником истины для

- конкретной задачи реализации;
- Scope и Out Of Scope задачи;
- требований, ограничений, зависимостей и критериев завершения задачи.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Backlog Task ID`;
- `Version`;
- `Creation Date`;
- `Author: Delivery Planner`;
- `Source Artifacts`.

### Objective

Конкретный результат, который должен быть достигнут.

Обязательные поля:

- `Objective`;
- `Expected Outcome`.

### Scope

Что входит в задачу.

Обязательные поля:

- `In Scope Items`.

### Out Of Scope

Что не входит в задачу.

Обязательные поля:

- `Out Of Scope Items`;
- `Reason`, если пункт может быть неоднозначным.

### Requirements

Требования, которые должна выполнить задача.

Для каждого требования обязательны поля:

- `Requirement`;
- `Source`;
- `Notes`.

### Constraints

Ограничения, обязательные для реализации задачи.

Для каждого ограничения обязательны поля:

- `Constraint`;
- `Source`;
- `Impact`.

### Dependencies

Зависимости задачи.

Для каждой зависимости обязательны поля:

- `Dependency`;
- `Type`;
- `Source`;
- `Reason`;
- `Impact`.

### Implementation Notes

Пояснения для Implementer, не меняющие архитектуру и не предписывающие код без необходимости.

Обязательные поля:

- `Note`;
- `Source`;

### Acceptance Criteria

Критерии завершения задачи.

Для каждого критерия обязательны поля:

- `Criterion`;
- `Verification Method`;
- `Source`.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Related Components`;
- `Related User Scenarios`;
- `Data Requirements`;
- `Integration Requirements`;
- `Risk Notes`;
- `Handoff Notes`.

Дополнительные разделы не должны менять PRD, Architecture Document или превращать Task Specification в реализацию.

---

# Artifact 07. Implementation Report

## Назначение

Фиксация фактических результатов реализации.

## Этап создания

Stage 6 — Implementation, после выполнения задачи или при фиксации блокера по задаче.

## Владелец

Implementer

## Является источником истины для

- фактической реализации конкретной задачи;
- изменённых файлов;
- добавленных или изменённых тестов;
- технических решений реализации;
- отклонений от Task Specification;
- известных проблем и найденного технического долга.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Backlog Task ID`;
- `Task Specification`;
- `Version`;
- `Creation Date`;
- `Author: Implementer`;
- `Source Artifacts`.

### Completed Work

Что реализовано.

Для каждого результата обязательны поля:

- `Item`;
- `Related Requirement`;
- `Related Acceptance Criteria`;
- `Notes`.

### Modified Files

Какие файлы изменены.

Для каждого файла обязательны поля:

- `File`;
- `Change Type`;
- `Summary`;
- `Related Requirement`.

### Tests Added

Какие тесты созданы или изменены.

Для каждого теста обязательны поля:

- `Test`;
- `Type`;
- `Covers`;
- `Result`.

Если тесты не созданы, раздел должен содержать причину.

### Acceptance Criteria Status

Статус выполнения критериев приёмки.

Для каждого критерия обязательны поля:

- `Criterion`;
- `Status`;
- `Verification Method`;
- `Evidence`;
- `Notes`.

### Technical Decisions

Принятые технические решения.

Для каждого решения обязательны поля:

- `Decision`;
- `Reason`;
- `Alternatives Considered`;
- `Consequences`;
- `Related Files`.

### Deviations

Отклонения от первоначального плана, Task Specification, ожидаемой области изменений или предполагаемого способа реализации.

Для каждого отклонения обязательны поля:

- `Deviation`;
- `Reason`;
- `Impact`;
- `Approved By`;
- `Follow-Up`.

Если отклонений нет, раздел должен содержать `None`.

### Technical Debt Found

Технический долг, обнаруженный во время реализации.

Для каждого пункта обязательны поля:

- `Debt`;
- `Location`;
- `Impact`;
- `Consequences`;
- `Recommendation`.

Если технический долг не обнаружен, раздел должен содержать `None`.

### Known Issues

Известные ограничения, дефекты, блокеры или непроверенные зоны.

Для каждого пункта обязательны поля:

- `Issue`;
- `Impact`;
- `Workaround`;
- `Required Follow-Up`.

Если известных проблем нет, раздел должен содержать `None`.

### Documentation Updated

Какая документация обновлена.

Для каждого документа обязательны поля:

- `Document`;
- `Change Summary`;
- `Reason`.

Если документация не обновлялась, раздел должен содержать причину или `Not Applicable`.

### Self-Check

Самопроверка готовности к Validation.

Обязательные поля:

- `Task implemented`;
- `Acceptance Criteria checked`;
- `Code builds`;
- `Tests pass`;
- `Documentation updated`;
- `Changes within scope`;
- `Ready for Validation`.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Build Notes`;
- `Manual Verification`;
- `Environment Notes`;
- `Follow-Up Suggestions`.

Дополнительные разделы не должны заменять Validation Report или скрывать незавершённую работу.

---

# Artifact 08. Validation Report

## Назначение

Результаты независимой проверки качества.

## Этап создания

Stage 7 — Validation

## Владелец

Validator

## Является источником истины для

- выполненных проверок;
- результатов проверки Scope и Acceptance Criteria;
- результатов проверки архитектурного соответствия;
- результатов проверки тестов;
- найденных дефектов, отклонений и наблюдений;
- остаточных рисков;
- итогового Validation Status;
- рекомендаций для Studio Director.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Validation Scope`;
- `Backlog Task ID`;
- `Task Specification`;
- `Implementation Report`;
- `Version`;
- `Creation Date`;
- `Author: Validator`;
- `Source Artifacts`.

### Executed Checks

Проведённые проверки.

Для каждой проверки обязательны поля:

- `Check`;
- `Source`;
- `Method`;
- `Result`;
- `Evidence`;
- `Notes`.

### Scope Validation

Проверка Scope, Out Of Scope, Constraints и Dependencies.

Для каждого элемента обязательны поля:

- `Item`;
- `Expected`;
- `Actual`;
- `Status`;
- `Evidence`;
- `Notes`.

### Acceptance Criteria Validation

Проверка каждого Acceptance Criterion.

Для каждого критерия обязательны поля:

- `Criterion`;
- `Status`;
- `Verification Method`;
- `Evidence`;
- `Rationale`;
- `Related Findings`.

Допустимые значения `Status`:

- `Passed`;
- `Passed With Notes`;
- `Failed`;
- `Not Verifiable`.

### Architecture Validation

Проверка соответствия Architecture Document.

Для каждого архитектурно значимого пункта обязательны поля:

- `Area`;
- `Expected`;
- `Actual`;
- `Status`;
- `Evidence`;
- `Notes`.

### Test Validation

Проверка тестов.

Для каждого набора тестов или теста обязательны поля:

- `Test`;
- `Type`;
- `Covers`;
- `Relevance`;
- `Execution Result`;
- `Gaps`;
- `Notes`.

### Findings

Обнаруженные проблемы, отклонения и наблюдения.

Для каждого finding обязательны поля:

- `Finding`;
- `Type`;
- `Severity`;
- `Source`;
- `Evidence`;
- `Impact`;
- `Recommendation`.

### Defect List

Дефекты, требующие исправления или решения.

Для каждого дефекта обязательны поля:

- `Defect`;
- `Severity`;
- `Impact`;
- `Source`;
- `Reproduction`;
- `Affected Artifacts`;
- `Evidence`;
- `Recommended Routing`.

Допустимые значения `Severity`:

- `Critical`;
- `Major`;
- `Minor`;
- `Observation`.

Если дефектов нет, раздел должен содержать `None`.

### Deviations

Отклонения от требований, архитектуры, Scope, Acceptance Criteria или Implementation Report.

Для каждого отклонения обязательны поля:

- `Deviation`;
- `Expected Baseline`;
- `Actual Result`;
- `Impact`;
- `Source Artifact`;
- `Requires Decision`;
- `Recommended Routing`.

Если отклонений нет, раздел должен содержать `None`.

### Risk Assessment

Остаточные риски.

Для каждого риска обязательны поля:

- `Risk`;
- `Probability`;
- `Impact`;
- `Mitigation`;
- `Owner`.

### Recommendations

Рекомендации для Studio Director.

Для каждой рекомендации обязательны поля:

- `Recommendation`;
- `Reason`;
- `Target Role`;
- `Target Stage`;
- `Priority`.

Если рекомендаций нет, раздел должен содержать `None`.

### Validation Status

Итоговый статус проверки.

Допустимые значения:

- `Passed`;
- `Passed With Risks`;
- `Failed`.

### Status Rationale

Краткое обоснование итогового статуса.

Обязательные поля:

- `Rationale`;
- `Blocking Findings`;
- `Risk Summary`.

### Required Follow-Up

Что должно произойти после Validation.

Для каждого действия обязательны поля:

- `Action`;
- `Owner`;
- `Target Stage`;
- `Reason`.

Если дальнейших действий нет, раздел должен содержать `None`.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Validation Environment`;
- `Manual Test Evidence`;
- `Automated Test Output`;
- `Traceability Notes`.

Дополнительные разделы не должны заменять обязательные выводы Validation Report.

---

# Artifact 09. Release Package

## Назначение

Описание релиза.

## Этап создания

Stage 9 — Release

## Владелец

Release Manager

## Является источником истины для

- состояния релиза;
- состава релиза;
- известных ограничений и рисков релиза;
- инструкций по развёртыванию;
- Release Notes для заказчика и пользователей.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Version`;
- `Date`;
- `Owner: Release Manager`;
- `Source Artifacts`.

### Release Scope

Границы релиза.

Обязательные поля:

- `Included`;
- `Excluded`, если важно для понимания границ;
- `Scope Notes`.

### Features

Реализованные возможности.

Для каждой возможности обязательны поля:

- `Feature ID or Name`;
- `Description`;
- `User or System Effect`;
- `Source`;
- `Validation Reference`.

### Bug Fixes

Исправленные дефекты.

Для каждого исправления обязательны поля:

- `Defect ID or Name`;
- `Fix Summary`;
- `Effect`;
- `Source`;
- `Validation Reference`.

Если исправлений нет, раздел должен содержать `None`.

### Validation Summary

Краткое резюме проверки релиза.

Обязательные поля:

- `Validation Status`;
- `Executed Checks Summary`;
- `Residual Risks`.

### Known Limitations

Известные ограничения релиза.

Для каждого ограничения обязательны поля:

- `Limitation`;
- `Impact`;
- `Source`;
- `Follow-Up`.

Если ограничений нет, раздел должен содержать `None`.

### Known Risks

Известные риски релиза.

Для каждого риска обязательны поля:

- `Risk`;
- `Likely Impact`;
- `Basis`;
- `Acceptance Status or Follow-Up`.

Если рисков нет, раздел должен содержать `None`.

### Deployment Instructions

Инструкции по развёртыванию.

Обязательные поля:

- `Environment`;
- `Dependencies`;
- `Configuration`;
- `Build`;
- `Run`;
- `Post-Deployment Check`;
- `Rollback`.

### Release Notes

Краткое описание изменений релиза для заказчика и пользователей.

Обязательные поля:

- `Summary`;
- `Main Changes`;
- `Known Limitations`;
- `Handoff Notes`.

### Related Artifacts

Связанные артефакты и служебные ссылки, подтверждающие релиз.

Обязательные ссылки:

- `Validation Report`;
- `Implementation Reports`;
- `Backlog`;
- `PRD`;
- `Architecture Document`;
- `Project State`, если применимо как служебная ссылка, а не как продуктовый артефакт.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Customer Handoff Notes`;
- `Traceability Matrix`;
- `Open Follow-Up Items`;
- `Operational Notes`.

Дополнительные разделы не должны включать неподтверждённую функциональность или заменять Validation Report.

---

# Artifact 10. Project Memory

## Назначение

Долговременная память проекта.

Project Memory Update является операцией обновления Project Memory, а не отдельным артефактом.

## Этап создания

На протяжении всего жизненного цикла проекта. Основной этап обновления — Stage 10 — Project Memory Update.

## Владелец

Historian

## Является источником истины для

- накопленных знаний проекта;
- причин ключевых решений;
- отклонённых альтернатив;
- технического долга;
- уроков проекта;
- будущих идей;
- исторического контекста, который неочевиден из текущего состояния артефактов.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Version`;
- `Last Updated`;
- `Owner: Historian`.

### Decisions

Ключевые решения.

Для каждого решения обязательны поля:

- `Decision ID`;
- `Decision`;
- `Date`;
- `Source`;
- `Owner`;
- `Reason`;
- `Alternatives Considered`;
- `Consequences`;
- `Related Artifacts`;
- `Status`.

### Decision Rationale

Причины решений, если они требуют отдельного объяснения за пределами записи в `Decisions`.

Обязательные поля:

- `Decision ID`;
- `Rationale`;
- `Context`;
- `Source`.

### Rejected Alternatives

Отклонённые варианты, которые важны для понимания будущих решений.

Обязательные поля:

- `Alternative`;
- `Rejected For`;
- `Decision ID or Source`;
- `Can Be Reconsidered: Yes/No`.

### Technical Debt

Технический долг.

Для каждого пункта обязательны поля:

- `Debt ID`;
- `Debt`;
- `Source`;
- `Location`;
- `Impact`;
- `Consequences`;
- `Recommended Action`;
- `Priority`;
- `Status`.

### Lessons Learned

Полученные знания.

Обязательные поля:

- `Lesson`;
- `Source`;
- `Applies To`;
- `Future Use`.

### Future Ideas

Идеи для развития.

Обязательные поля:

- `Idea`;
- `Source`;
- `Potential Value`;
- `Status`.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Active Constraints`;
- `Known Risks`;
- `Context Notes`;
- `Superseded Decisions`.

### Active Constraints

Условно обязательный раздел, если в проекте есть активные ограничения, которые должны учитываться будущими агентами.

Для каждого ограничения обязательны поля:

- `Constraint`;
- `Source`;
- `Impact`;
- `Owner`;
- `Status`.

### Known Risks

Условно обязательный раздел, если существуют риски, важные для будущей работы.

Для каждого риска обязательны поля:

- `Risk`;
- `Source`;
- `Impact`;
- `Mitigation`;
- `Status`.

### Context Notes

Дополнительный раздел для компактных заметок, которые помогают восстановить контекст.

Для каждой заметки обязательны поля:

- `Note`;
- `Source`;
- `Why It Matters`.

### Superseded Decisions

Условно обязательный раздел, если ранее принятые решения были заменены.

Для каждой записи обязательны поля:

- `Original Decision ID`;
- `Superseded By`;
- `Reason`;
- `Date`;
- `Source`.

Project Memory не должен становиться копией PRD, Architecture Document, Backlog, Task Specifications, Implementation Reports, Validation Reports или Release Package.

---

# Зависимости артефактов

```text
Idea Brief
    ↓

Discovery Report
    ↓

PRD
    ↓

Architecture Document
    ↓

Backlog
    ↓

Task Specification
    ↓

Implementation Report
    ↓

Validation Report
    ↓

Release Package

Project Memory
    ↑
Получает информацию со всех этапов
```

---

# Материалы согласования

Материалы согласования используются для принятия решений на отдельных этапах жизненного цикла, но не входят в канонический перечень артефактов проекта.

## Release Candidate Summary

Release Candidate Summary — обязательный материал согласования на этапе RELEASE APPROVAL.

Release Candidate Summary не является каноническим артефактом проекта.

Release Candidate Summary не является источником истины для:

- требований;
- реализации;
- проверки качества;
- состояния релиза;
- Project Memory.

Release Candidate Summary существует для customer-facing согласования release candidate. Он должен кратко показать заказчику, что реализовано, что не реализовано, какие результаты Validation получены, какие ограничения и риски известны и какое решение требуется принять.

Release Candidate Summary собирается из канонических источников и служебных решений. Он не должен вводить новые требования, менять результаты Validation, переопределять состав реализации или заменять Release Package.

Обязательные источники Release Candidate Summary:

- PRD;
- Validation Report;
- Implementation Reports, если нужны для состава реализованного;
- Backlog, если нужен для связи с выполненными работами;
- Project State;
- связанные решения Studio Director.

После решения заказчика результат RELEASE APPROVAL фиксируется в Project State.

После RELEASE состояние релиза фиксируется в Release Package.

### Минимальная структура

Release Candidate Summary должен содержать:

- `Metadata`;
- `Release Candidate Scope`;
- `Implemented Items`;
- `Not Implemented`;
- `Validation Summary`;
- `Known Limitations`;
- `Known Risks`;
- `Deviations From Plan`;
- `Decision Request`.

Детальный процесс использования Release Candidate Summary на этапе RELEASE APPROVAL определён в `RELEASE_APPROVAL.md`.

---

# Служебные объекты

## Project State

Project State — служебное состояние проекта, которым управляет Studio Director.

Project State не является продуктовым артефактом и не входит в канонический перечень артефактов проекта.

Project State существует для оркестрации процесса и хранит только состояние процесса: текущий этап, статус, назначение, ссылки на активные артефакты, блокеры, эскалацию, текущую цель и последние процессные решения.

Каноническая структура Project State определена в `PROJECT_STATE.md`.

## Владелец

Studio Director

Project State не должен дублировать содержимое канонических артефактов. Он хранит ссылки, статусы и решения, необходимые для маршрутизации работы.

---

# Минимальный набор артефактов проекта

Проект не может перейти к реализации при отсутствии:

- PRD
- Architecture Document
- Backlog

---

# Канонические артефакты проекта

Независимо от размера проекта обязательно должны существовать:

1. PRD
2. Architecture Document
3. Backlog
4. Project Memory

Эти артефакты образуют ядро знаний проекта.

Удаление или потеря любого из них считается критическим дефектом процесса.
