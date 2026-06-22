# ARTIFACTS.md
v0.2
2026-06-22

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

## Source Of Work

`Source Of Work` обязателен для задач реализации.

`Source Artifacts` объясняет, из каких документов создан артефакт. `Source Of Work` объясняет, почему конкретная задача имеет право существовать.

Допустимые источники задач:

- Mission;
- roadmap;
- review;
- bug report;
- технический долг;
- change request;
- решение Product Owner;
- решение Studio Director;
- результат Validator;
- результат Release Review;
- явно зафиксированный проектный артефакт.

Если Mission используется как Source Of Work, задача должна содержать trace:

```text
Mission → Roadmap / Review / Backlog Item → Task
```

Trace должен показывать не только Mission ID, но и исходный roadmap, review, backlog item, решение или другой подтверждённый источник, из которого появилась задача внутри Mission.

Если Source Of Work для задачи отсутствует, задача не должна попадать в Backlog, Task Specification или Codex task. Владелец планирования должен вернуть запрос на уточнение или подготовить эскалацию через Studio Director.

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
- предложенного решения и его связи с проблемой;
- пользователей и ролей;
- пользовательских, административных и операционных сценариев, выявленных на Discovery;
- пропущенных требований, слепых зон и пограничных случаев;
- критериев и метрик успеха;
- ограничений, допущений, рисков и открытых вопросов, выявленных на Discovery;
- рекомендаций Product Analyst перед созданием PRD.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Version`;
- `Creation Date`;
- `Author: Product Analyst`;
- `Source Artifacts`.

### Problem Understanding

Какую проблему нужно решить и какой контекст влияет на её понимание.

Обязательные поля:

- `Problem`;
- `Business Context`;
- `Known Goals`;
- `Known Constraints`;
- `Evidence or Source`.

### Proposed Solution Understanding

Какое решение предложено заказчиком, если оно уже есть, и насколько оно связано с реальной проблемой.

Обязательные поля:

- `Customer Proposed Solution`, если заказчик предложил решение;
- `Problem-Solution Fit`;
- `Contradictions or Weak Fit`, если они обнаружены;
- `Relevant Alternatives`, если очевидные альтернативы важны для риска или бизнес-эффекта.

### Users and Roles

Для кого создаётся продукт и какие роли нужны для его использования, администрирования, эксплуатации или поддержки.

Обязательные поля:

- `Role or User Group`;
- `Goal or Responsibility`;
- `Context of Use`;
- `Status: Known, Assumed, or Missing`;
- `Priority or Impact`, если ролей несколько.

### Missing Requirements and Blind Spots

Каких требований, ролей, сценариев, процессов, механизмов или условий не хватает в исходном описании.

Обязательные поля:

- `Blind Spot`;
- `Category: Requirement, Role, User Scenario, Administrative Scenario, Operational Process, Support, Maintenance, Monitoring, Success Metric, Edge Case, or Risk`;
- `Why It Matters`;
- `Impact on PRD`;
- `Recommended Follow-Up`.

### User Scenarios

Какие пользовательские сценарии известны, предполагаются или отсутствуют.

Обязательные поля:

- `Scenario`;
- `User or Role`;
- `Expected Outcome`;
- `Status: Known, Assumed, or Missing`;
- `Edge Cases`, если применимо.

### Administrative and Operational Scenarios

Какие административные сценарии, операционные процессы и эксплуатационные действия нужны или могут быть нужны.

Обязательные поля:

- `Scenario or Process`;
- `Responsible Role`;
- `Trigger`;
- `Expected Outcome`;
- `Missing Information or Risk`.

### Support and Maintenance Considerations

Какие процессы поддержки, сопровождения, мониторинга и обработки проблем нужны или могут быть нужны.

Обязательные поля:

- `Need`;
- `Operational Owner`, если известен;
- `Monitoring or Support Mechanism`;
- `Failure or Issue Handling`;
- `Follow-Up`.

### Success Metrics

Что считается успешным результатом и как это можно измерить или подтвердить.

Обязательные поля:

- `Metric or Criterion`;
- `Measurement or Evidence`;
- `Source`;
- `Validation Need`, если требуется последующая проверка.

### Risks and Assumptions

Риски, допущения и открытые вопросы, влияющие на бизнес-результат, продукт, архитектуру, внедрение, масштабирование или эксплуатацию.

Обязательные поля:

- `Type: Risk, Assumption, or Open Question`;
- `Statement`;
- `Cause or Reason`;
- `Impact`;
- `Likelihood or Severity`, если это риск;
- `Mitigation, Validation Need, or Routing`.

### Recommendations Before PRD

Что Product Analyst рекомендует уточнить, добавить, проверить или явно передать Product Owner перед созданием PRD.

Обязательные поля:

- `Recommendation`;
- `Reason`;
- `Owner or Routing`;
- `Impact on PRD`;
- `Priority`.

Рекомендации Product Analyst не являются PRD, не утверждают финальный состав продукта и не переносят владение требованиями от Product Owner.

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
- Source Of Work каждой задачи;
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
- `Source Of Work`;
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
- Source Of Work задачи;
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

### Source Of Work

Подтверждённый источник появления задачи.

Обязательные поля:

- `Source`;
- `Source Type`;
- `Source Reference`;
- `Trace`.

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
- результатов Compliance Review;
- результатов Expert Review;
- найденных дефектов, рисков, улучшений и субъективных предпочтений;
- возможностей улучшения;
- остаточных рисков;
- итогового Validation Verdict;
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

### Compliance Review

Проверка соответствия: сделано ли то, что было заказано.

Обязательные поля:

- `Requirements / PRD`;
- `Acceptance Criteria`;
- `Architecture Constraints`;
- `Implemented Scope`;
- `Out Of Scope`;
- `Test Evidence`;
- `Compliance Result`;
- `Blocking Issues`;
- `Evidence`.

Допустимые значения `Compliance Result`:

- `Passed`;
- `Passed With Notes`;
- `Failed`;
- `Not Verifiable`.

### Expert Review

Экспертная оценка качества: насколько хорошим получилось решение.

Обязательные поля:

- `Architecture Quality`;
- `Code Quality`;
- `Maintainability`;
- `Dependency Review`;
- `Security`;
- `Testability`;
- `Test Coverage Review`;
- `Technical Debt`;
- `Scalability`;
- `Solution Complexity`;
- `UX`, если применимо;
- `Expert Review Result`;
- `Blocking Quality Issues`;
- `Non-Blocking Quality Notes`;
- `Evidence`.

Допустимые значения `Expert Review Result`:

- `Acceptable`;
- `Acceptable With Risks`;
- `Needs Improvement`;
- `Not Assessed`.

Expert Review не должен автоматически блокировать релиз только потому, что существует более предпочтительный вариант реализации. Блокирующим может быть только finding с типом `Defect` или существенный `Risk`, имеющий проверяемое влияние.

### Findings

Обнаруженные дефекты, риски, улучшения и субъективные предпочтения.

Для каждого finding обязательны поля:

- `Finding`;
- `Type`;
- `Review Mode`;
- `Severity`;
- `Blocking`;
- `Source`;
- `Evidence`;
- `Impact`;
- `Recommendation`.

Допустимые значения `Type`:

- `Defect`;
- `Risk`;
- `Improvement`;
- `Subjective Preference`.

Допустимые значения `Review Mode`:

- `Compliance Review`;
- `Expert Review`.

Допустимые значения `Severity`:

- `Critical`;
- `Major`;
- `Minor`;
- `Observation`.

Если findings нет, раздел должен содержать `None`.

### Improvement Opportunities

Неблокирующие возможности улучшения.

Для каждой возможности обязательны поля:

- `Opportunity`;
- `Related Finding`;
- `Expected Benefit`;
- `Why Non-Blocking`;
- `Suggested Owner`;
- `Priority`.

Если возможностей улучшения нет, раздел должен содержать `None`.

Improvement Opportunities не являются дефектами и не должны становиться обязательным возвратом в Implementation без отдельного решения Studio Director.

### Validation Verdict

Итоговое проверочное решение.

Обязательные поля:

- `Compliance Review Result`;
- `Expert Review Result`;
- `Validation Status`;
- `Blocking Findings`;
- `Non-Blocking Risks`;
- `Improvement Opportunities Summary`;
- `Subjective Preferences Summary`;
- `Required Follow-Up`;
- `Status Rationale`.

Допустимые значения `Validation Status`:

- `Passed`;
- `Passed With Risks`;
- `Failed`.

`Improvement` и `Subjective Preference` не являются блокерами Validation сами по себе.

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

# Artifact 11. Audit Intake Brief

## Назначение

Audit Intake Brief фиксирует запуск аудита существующего проекта в режиме Existing Project Review.

Он нужен, чтобы Studio Director мог начать аудит без ручного придумывания процесса, согласовать границы проверки и явно показать, какие входные данные доступны, чего не хватает и какие ограничения есть у review.

Audit Intake Brief создаётся только для отдельного режима Existing Project Review, описанного в `EXISTING_PROJECT_REVIEW.md`.

Он не является обязательным артефактом основного жизненного цикла разработки.

## Этап создания

Отдельный режим — Existing Project Review, до начала Audit.

Не является этапом из `LIFECYCLE.md`.

## Владелец

Studio Director.

Studio Director может подготовить Audit Intake Brief на основании запроса заказчика, ссылки на репозиторий, переданных файлов, документации или другого входного контекста.

## Является источником истины для

- запуска Existing Project Review;
- цели аудита;
- границ аудита;
- доступных входных источников;
- отсутствующих входных источников;
- ограничений аудита;
- запрошенной глубины review;
- запрошенных deliverables.

Audit Intake Brief не заменяет Existing Project Review Report, PRD, Architecture Document, Validation Report или Project Memory.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Version`;
- `Creation Date`;
- `Prepared By`;
- `Request Source`.

### Project Name

Название существующего проекта или системы.

### Audit Goal

Зачем проводится аудит и какое решение должен помочь принять результат.

### Audit Scope

Какая система, часть системы, репозиторий, компонент, продуктовая область или набор вопросов входит в review.

Scope должен также фиксировать явно исключённые области, если они важны для ожиданий заказчика.

### Available Inputs

Доступные источники анализа.

Минимальное обязательное условие запуска аудита — хотя бы один источник анализа.

Источником анализа может быть репозиторий, исходный код, документация, архитектурный документ, описание системы, список известных проблем, результаты CI, эксплуатационные заметки или другой проверяемый контекст.

### Missing Inputs

Входные данные, которые были бы полезны, но отсутствуют на момент запуска review.

Отсутствующие материалы не всегда блокируют аудит, но должны быть явно видны до начала работы.

### Audit Limitations

Ограничения проверки, вызванные неполным scope, отсутствием запуска, отсутствием тестовых данных, отсутствием инфраструктуры, неполной документацией или другими условиями.

Если review выполняется только по статическим источникам, это должно быть указано здесь.

### Requested Depth

Запрошенная глубина аудита.

Допустимые значения:

- `Light Review` — быстрый обзор для первичного понимания состояния проекта;
- `Standard Review` — полноценный аудит по доступным входным данным;
- `Deep Review` — максимально возможный анализ в рамках доступов, времени и scope.

### Requested Deliverables

Ожидаемые результаты review.

Минимальный итоговый deliverable для режима Existing Project Review — Existing Project Review Report.

Дополнительные deliverables допускаются только как уточнение формата вывода и не создают новые обязательные роли или этапы lifecycle.

### Input Classification

Обязательные входные данные:

- хотя бы один источник анализа.

Необязательные входные данные:

- документация;
- архитектурные документы;
- доступ к запуску;
- тестовые данные;
- инфраструктура.

Необязательные входные данные могут существенно влиять на точность review. Если они отсутствуют, ограничение должно быть отражено в `Missing Inputs` и `Audit Limitations`.

---

# Artifact 12. Existing Project Review Report

## Назначение

Структурированный результат аудита существующего проекта.

Existing Project Review Report создаётся только в режиме Existing Project Review, описанном в `EXISTING_PROJECT_REVIEW.md`.

Он не является обязательным артефактом основного жизненного цикла разработки.

## Этап создания

Отдельный режим — Existing Project Review.

Не является этапом из `LIFECYCLE.md`.

## Владелец

Назначенная Studio Director роль из существующего набора ролей.

По умолчанию итоговую сборку отчёта выполняет Validator, если review включает Quality Review.

Product Analyst отвечает за содержимое раздела `Product Review`.

Solution Architect отвечает за содержимое раздела `Architecture Review`.

Validator отвечает за содержимое раздела `Quality Review` и применение `CODE_REVIEW_FRAMEWORK.md`.

Studio Director оркестрирует режим, но не становится новой ролью аудита.

## Является источником истины для

- выводов аудита существующего проекта;
- продуктовых проблем и отсутствующих сценариев;
- архитектурных рисков;
- quality findings;
- рисков эксплуатации, поддержки и развития;
- возможностей улучшения;
- recommended roadmap.

Existing Project Review Report не заменяет PRD, Architecture Document, Backlog, Validation Report, Release Package или Project Memory.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Reviewed System`;
- `Audit Intake Brief`;
- `Review Scope`;
- `Version`;
- `Creation Date`;
- `Report Owner`;
- `Participating Roles`;
- `Source Inputs`;
- `Limitations`.

`Source Inputs` должен перечислять репозиторий, код, документацию, архитектурные документы, описание системы или другие входы, использованные при review.

`Audit Intake Brief` должен ссылаться на стартовый intake или эквивалентное процессное решение Studio Director.

### Executive Summary

Краткий вывод по состоянию существующего проекта.

Обязательные поля:

- `Overall Assessment`;
- `Top Findings`;
- `Primary Risks`;
- `Highest-Value Improvements`;
- `Recommended Next Step`.

### Product Review

Выводы Product Analyst по продуктовой стороне существующей системы.

Для каждого вывода обязательны поля:

- `Observation`;
- `Consequence`;
- `Recommendation`.

Если Product Review не применим, раздел должен содержать `Not Applicable` и причину.

### Architecture Review

Выводы Solution Architect по архитектуре и техническим решениям.

Для каждого вывода обязательны поля:

- `Observation`;
- `Consequence`;
- `Recommendation`.

Если Architecture Review не применим, раздел должен содержать `Not Applicable` и причину.

### Quality Review

Выводы Validator по качеству реализации с использованием `CODE_REVIEW_FRAMEWORK.md`.

Для каждого вывода обязательны поля:

- `Observation`;
- `Consequence`;
- `Recommendation`;
- `Finding Type: Defect, Risk, Improvement, or Subjective Preference`;
- `Severity: Critical, Major, Minor, or Observation`;
- `Evidence`.

Если Quality Review не применим, раздел должен содержать `Not Applicable` и причину.

### Risks

Риски эксплуатации, развития, поддержки, безопасности, масштабирования, продукта или архитектуры.

Для каждого риска обязательны поля:

- `Risk`;
- `Source`;
- `Consequence`;
- `Severity`;
- `Recommended Mitigation`;
- `Owner or Routing`.

Если рисков нет, раздел должен содержать `None`.

### Improvement Opportunities

Список улучшений, отделённых от дефектов.

Для каждого улучшения обязательны поля:

- `Opportunity`;
- `Observation`;
- `Consequence`;
- `Recommendation`;
- `Expected Benefit`;
- `Priority`.

Если улучшений нет, раздел должен содержать `None`.

### Recommended Roadmap

Предлагаемый план развития существующей системы.

Обязательные группы:

- `Critical Fixes`;
- `Risk Reduction`;
- `Product Gaps`;
- `Architecture Improvements`;
- `Quality Improvements`;
- `Operational Improvements`;
- `Later Opportunities`.

Для каждого пункта roadmap обязательны поля:

- `Item`;
- `Reason`;
- `Expected Outcome`;
- `Suggested Owner or Role`;
- `Priority`;
- `Dependencies`, если есть.

Recommended Roadmap не является Backlog и не создаёт обязательства реализации.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Reviewed Inputs`;
- `Out Of Scope`;
- `Open Questions`;
- `Appendix`.

Дополнительные разделы не должны заменять обязательные разделы или превращать отчёт в полный пересказ кода.

---

# Artifact 13. Mission Definition and Plan (`MISSION.md`)

## Назначение

Mission Definition and Plan фиксирует запуск Mission Mode для крупной цели, которая не выполняется одной задачей и может порождать несколько связанных Task.

Mission является надстройкой над Task Mode. Mission не является Task, не заменяет Backlog или Task Specification и не даёт права менять vision, roadmap, продуктовую стратегию или продуктовые решения.

`MISSION.md` создаётся только для активной Mission.

## Этап создания

Отдельный режим — Mission Mode, Mission Intake и Mission Planning.

Не является этапом из `LIFECYCLE.md`.

## Владелец

Studio Director.

Studio Director может подготовить Mission Definition and Plan на основании запроса заказчика, roadmap, review, решения Product Owner, решения Studio Director или другого допустимого Source Of Work.

## Является источником истины для

- Mission ID;
- цели Mission;
- описания Mission;
- входных артефактов;
- scope boundaries;
- ограничений Mission;
- критериев завершения;
- stop conditions;
- бюджета автономности;
- milestones;
- правил остановки и эскалации Mission.

Mission Definition and Plan не заменяет PRD, Architecture Document, Backlog, Task Specification, Validation Report, Release Package или Project Memory.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Mission ID`;
- `Version`;
- `Creation Date`;
- `Author: Studio Director`;
- `Source Artifacts`;
- `Source Of Work`;

### Mission Summary

Краткое описание Mission.

Обязательные поля:

- `Title`;
- `Goal`;
- `Description`;
- `Expected Outcome`.

### Mission Boundaries

Границы Mission.

Обязательные поля:

- `In Scope`;
- `Out Of Scope`;
- `Scope Protection`;
- `Forbidden Changes`.

`Scope Protection` должен явно фиксировать, что Mission не может расширять roadmap, менять vision, добавлять крупные функции вне roadmap или менять продуктовую стратегию.

### Input Artifacts

Входные источники Mission.

Для каждого источника обязательны поля:

- `Artifact or Input`;
- `Path or Reference`;
- `Role In Mission`;
- `Status`;
- `Limitations`, если есть.

### Mission Lifecycle

Служебный lifecycle Mission.

Обязательные этапы:

- `Mission Intake`;
- `Mission Planning`;
- `Backlog Generation`;
- `Implementation Loop`;
- `Mission Review`;
- `Mission Complete`.

Для каждого этапа обязательны поля:

- `Purpose`;
- `Inputs`;
- `Outputs`;
- `Responsible Role`.

### Milestones

Целевые milestones Mission.

Для каждого milestone обязательны поля:

- `Milestone`;
- `Completion Criteria`;
- `Related Source`;
- `Expected Tasks`, если известны.

### Autonomy Budget

Бюджет автономности Mission.

Обязательные поля:

- `Task Limit`;
- `Cycle Limit`;
- `File Change Limit`, если применимо;
- `Time Limit`, если применимо;
- `Other Limits`, если есть;
- `Budget Exhaustion Rule`.

### Stop Conditions

Условия обязательной остановки Mission.

Обязательные условия:

- требуется продуктовое решение;
- найден архитектурный блокер;
- roadmap противоречит проекту;
- есть несколько равноценных направлений развития;
- достигнут milestone;
- исчерпан бюджет автономности.

### Completion Criteria

Критерии завершения Mission.

Для каждого критерия обязательны поля:

- `Criterion`;
- `Verification Method`;
- `Source`.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Assumptions`;
- `Known Risks`;
- `Pilot Reference`;
- `Open Questions`.

Дополнительные разделы не должны превращать Mission в PRD, roadmap, Architecture Document, Backlog или Task Specification.

---

# Artifact 14. Mission State (`MISSION_STATE.md`)

## Назначение

Mission State фиксирует текущее служебное состояние активной Mission.

Mission State нужен, чтобы Studio Director мог продолжать Mission между циклами, видеть текущий milestone, активную задачу, использованный бюджет автономности, блокеры и последнее решение.

`MISSION_STATE.md` создаётся только для активной Mission.

## Этап создания

Отдельный режим — Mission Mode, начиная с Mission Planning и далее на протяжении Mission.

Не является этапом из `LIFECYCLE.md`.

## Владелец

Studio Director.

## Является источником истины для

- текущего статуса Mission;
- текущего milestone;
- текущего цикла;
- текущей или следующей задачи;
- использованного бюджета автономности;
- активных блокеров;
- активных stop conditions;
- последнего Mission Review;
- следующего процессного решения Mission.

Mission State не заменяет Project State. Project State может ссылаться на активную Mission, но не должен копировать содержимое `MISSION_STATE.md`.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Mission ID`;
- `Version`;
- `Last Updated`;
- `Author: Studio Director`;
- `Source Artifacts`.

### Current Mission Status

Обязательные поля:

- `Status`;
- `Current Milestone`;
- `Current Cycle`;
- `Current Task`;
- `Next Task`;
- `Current Objective`.

Допустимые значения `Status`:

- `Not Started`;
- `In Planning`;
- `In Progress`;
- `Paused`;
- `Blocked`;
- `Waiting For Decision`;
- `Completed`;
- `Stopped`.

### Autonomy Budget Usage

Обязательные поля:

- `Task Limit`;
- `Tasks Completed`;
- `Cycle Limit`;
- `Cycles Completed`;
- `File Change Limit`, если применимо;
- `Files Changed`, если применимо;
- `Time Limit`, если применимо;
- `Time Used`, если применимо;
- `Budget Status`.

### Active Artifacts

Для каждого активного артефакта обязательны поля:

- `Artifact`;
- `Path or Reference`;
- `Owner`;
- `Status`;
- `Purpose In Mission`.

### Stop Condition Check

Для каждого stop condition обязательны поля:

- `Condition`;
- `Status`;
- `Evidence`;
- `Required Action`.

### Blocking Issues

Если блокеров нет, раздел должен содержать `None`.

Для каждого блокера обязательны поля:

- `ID`;
- `Description`;
- `Source`;
- `Owner`;
- `Impact`;
- `Recommended Action`.

### Last Mission Review

Обязательные поля:

- `Review Reference`;
- `Review Date`;
- `Decision`;
- `Next Step`.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Notes`;
- `Risk Snapshot`;
- `Opportunity Snapshot`.

Дополнительные разделы не должны заменять `MISSION_REVIEW.md`, Backlog, Task Specification или Project Memory.

---

# Artifact 15. Mission Backlog (`MISSION_BACKLOG.md`)

## Назначение

Mission Backlog фиксирует связанные задачи внутри конкретной Mission.

Mission Backlog является Mission-specific представлением работ. Он не заменяет общий Backlog проекта и не отменяет Task Specifications. Каждая задача из Mission Backlog, переданная в реализацию, должна иметь обычную Task Specification.

`MISSION_BACKLOG.md` создаётся только для активной Mission.

## Этап создания

Отдельный режим — Mission Mode, Backlog Generation и дальнейшие обновления во время Mission Review.

Не является этапом из `LIFECYCLE.md`.

## Владелец

Delivery Planner.

## Является источником истины для

- списка задач конкретной Mission;
- порядка выполнения задач Mission;
- зависимостей между задачами Mission;
- Source Of Work и trace каждой задачи Mission;
- связи задач Mission с roadmap, review, Backlog item или другим подтверждённым источником;
- статуса задач внутри Mission.

Mission Backlog не заменяет PRD, Architecture Document, общий Backlog проекта, Task Specification или Validation Report.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Mission ID`;
- `Version`;
- `Creation Date`;
- `Author: Delivery Planner`;
- `Source Artifacts`;
- `Mission Definition`.

### Mission Work Summary

Обязательные поля:

- `Mission Goal`;
- `Execution Strategy`;
- `Key Dependencies`;
- `Known Risks`.

### Mission Tasks

Для каждой задачи обязательны поля:

- `Task ID`;
- `Title`;
- `Source Of Work`;
- `Trace`;
- `Description`;
- `Owner`;
- `Related Mission Milestone`;
- `Related Roadmap / Review / Backlog Item`;
- `Dependencies`;
- `Status`;
- `Stop Condition Risk`, если есть.

`Trace` должен соответствовать формату:

```text
Mission → Roadmap / Review / Backlog Item → Task
```

Допустимые значения `Status`:

- `Planned`;
- `Ready`;
- `In Progress`;
- `Validation`;
- `Done`;
- `Blocked`.

Допустимые переходы статусов:

- `Planned` → `Ready`, когда зависимости закрыты и Source Of Work подтверждён.
- `Ready` → `In Progress`, когда Studio Director запускает Single-Step цикл и назначает Implementer через Task Specification.
- `In Progress` → `Validation`, когда Implementer завершил работу и подготовил Implementation Report.
- `Validation` → `Done`, когда Validator подтвердил результат.
- `Validation` → `Blocked`, если Validator отклонил результат или требуется решение другой роли.
- `Ready` → `Blocked`, если перед стартом обнаружен stop condition, budget issue, продуктовый вопрос или архитектурный риск.
- `In Progress` → `Blocked`, если Implementer обнаружил blocker, выход за scope или необходимость решения Product Owner / Solution Architect.

В Single-Step режиме после любого перехода в `Done` или `Blocked` Mission обязана остановиться и зафиксировать Mission Execution Record.

### Execution Order

Для каждого шага обязательны поля:

- `Order`;
- `Task ID`;
- `Reason`;
- `Can Run In Parallel With`;
- `Blocks`.

### Mission Dependencies

Для каждой зависимости обязательны поля:

- `Dependent Task`;
- `Dependency Source`;
- `Dependency Type`;
- `Reason`;
- `Impact On Mission`.

### Scope Protection Check

Обязательные поля:

- `Roadmap Boundary`;
- `Product Boundary`;
- `Architecture Boundary`;
- `Out Of Scope Work`;
- `Potential Opportunities`.

Новые идеи должны попадать в `Potential Opportunities`, а не в список задач Mission без решения Product Owner.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Milestone Map`;
- `Blocked Items`;
- `Planning Assumptions`;
- `Rework Items`.

Дополнительные разделы не должны превращать Mission Backlog в roadmap, PRD, Architecture Document или Implementation Report.

---

# Artifact 16. Mission Review (`MISSION_REVIEW.md`)

## Назначение

Mission Review фиксирует обзор Mission после цикла, milestone, блокера, исчерпания бюджета автономности или завершения Mission.

Mission Review нужен, чтобы Studio Director мог принять процессное решение: продолжить Mission, остановить Mission, завершить Mission, подготовить эскалацию или открыть новую Mission.

`MISSION_REVIEW.md` создаётся только для активной Mission.

## Этап создания

Отдельный режим — Mission Mode, Mission Review и Mission Complete.

Не является этапом из `LIFECYCLE.md`.

## Владелец

Studio Director.

Studio Director может использовать входы Delivery Planner, Validator, Implementer и Historian, но итоговое процессное решение Mission Review остаётся за Studio Director.

## Является источником истины для

- результата очередного Mission cycle;
- записей выполнения Mission cycle;
- выполненных задач;
- validation status выполненных задач;
- оставшихся задач;
- новых рисков;
- stop condition check;
- использованного бюджета автономности;
- найденных Opportunities;
- решения о продолжении, остановке или завершении Mission.

Mission Review не заменяет Validation Report, Implementation Report, Mission Backlog, Mission State или Project Memory.

## Каноническая структура

### Metadata

Обязательные поля:

- `Project ID`;
- `Mission ID`;
- `Review ID`;
- `Version`;
- `Creation Date`;
- `Author: Studio Director`;
- `Source Artifacts`.

### Review Scope

Обязательные поля:

- `Reviewed Cycle`;
- `Reviewed Milestone`;
- `Reviewed Tasks`;
- `Input Artifacts`;
- `Limitations`, если есть.

### Completed Work

Для каждой завершённой задачи обязательны поля:

- `Task ID`;
- `Title`;
- `Source Of Work`;
- `Validation Result`;
- `Result Summary`;
- `Related Artifacts`.

### Mission Execution Records

Записи выполнения Mission cycle.

Для каждого цикла обязательны поля:

- `Execution ID`;
- `Cycle`;
- `Backlog Item`;
- `Started At`;
- `Completed At`;
- `Assigned Roles`;
- `Executor Summary`;
- `Result`;
- `Status`;
- `Changed Artifacts`;
- `Validation Result`;
- `New Risks`;
- `New Source Of Work`;
- `Stop Reason`;

Если Mission ещё не выполняла ни одного цикла, раздел должен содержать `None`.

В Single-Step режиме один Mission Execution Record соответствует одной backlog item.

### Remaining Work

Для каждой оставшейся задачи обязательны поля:

- `Task ID`;
- `Title`;
- `Status`;
- `Dependency`;
- `Risk`;
- `Recommended Next Step`.

### Risk and Blocker Review

Для каждого риска или блокера обязательны поля:

- `Item`;
- `Type`;
- `Source`;
- `Impact`;
- `Owner or Routing`;
- `Required Action`.

Если рисков и блокеров нет, раздел должен содержать `None`.

### Autonomy Budget Review

Обязательные поля:

- `Tasks Completed`;
- `Cycles Completed`;
- `Files Changed`, если применимо;
- `Time Used`, если применимо;
- `Budget Status`;
- `Budget Exhausted: Yes / No`.

### Stop Condition Review

Для каждого stop condition обязательны поля:

- `Condition`;
- `Triggered: Yes / No`;
- `Evidence`;
- `Decision`.

### Opportunities

Новые идеи и возможности, найденные во время Mission.

Для каждой Opportunity обязательны поля:

- `Opportunity`;
- `Source`;
- `Why Out Of Mission Scope`;
- `Suggested Owner`;
- `Required Decision`.

Если Opportunities нет, раздел должен содержать `None`.

### Mission Decision

Обязательные поля:

- `Decision`;
- `Decision Maker`;
- `Reason`;
- `Next Step`;
- `Required Artifact Updates`.

Допустимые значения `Decision`:

- `Continue Mission`;
- `Pause Mission`;
- `Stop Mission`;
- `Complete Mission`;
- `Escalate`;
- `Open New Mission`.

## Дополнительные разделы

Допустимые дополнительные разделы:

- `Validation Summary`;
- `Implementation Summary`;
- `Lessons Learned`;
- `Project Memory Update Request`.

Дополнительные разделы не должны заменять Validation Report, Implementation Report или Project Memory.

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

Audit Intake Brief
    ↓

Existing Project Review Report
    ↑
Создаётся только в отдельном режиме Existing Project Review

Mission Definition and Plan
    ↓

Mission State
    ↔

Mission Backlog
    ↓

Task Specification
    ↓

Implementation Report
    ↓

Validation Report
    ↓

Mission Review
    ↑
Создаётся только в отдельном режиме Mission Mode
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

---

# Минимальный набор артефактов Mission Mode

Если Mission Mode не активен, Mission-артефакты не требуются.

Если Mission Mode активен, должны существовать:

1. `MISSION.md`
2. `MISSION_STATE.md`
3. `MISSION_BACKLOG.md`
4. `MISSION_REVIEW.md` после первого Mission Review или завершения первого цикла

Mission-артефакты не заменяют PRD, Architecture Document, Backlog, Task Specifications, Implementation Reports, Validation Reports, Release Package или Project Memory.

Потеря Mission-артефакта активной Mission считается дефектом оркестрации Mission Mode, но не меняет обязательный минимальный набор обычного Task Mode.
