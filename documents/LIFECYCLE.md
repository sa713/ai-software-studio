# LIFECYCLE.md
v0.4
2026-06-19

## Назначение

Данный документ определяет единственный допустимый жизненный цикл продукта внутри AI Software Studio.

Все агенты обязаны следовать данному процессу.

Переход между этапами допускается только при выполнении критериев завершения текущего этапа либо при явном решении о возврате на предыдущий этап.

Studio Director фиксирует текущее состояние процесса в Project State. Project State является служебным состоянием оркестратора, а не этапом жизненного цикла и не продуктовым артефактом. Каноническая модель Project State определена в `PROJECT_STATE.md`.

---

# Режимы работы

AI Software Studio поддерживает два режима работы:

- Task Mode;
- Mission Mode.

Task Mode является основным режимом работы Студии. В Task Mode Студия выполняет отдельные задачи через обычную цепочку Source Of Work → Task → Implementation → Validation.

Mission Mode является надстройкой над Task Mode. Он предназначен для автономного достижения крупной цели, которая не выполняется одной задачей и порождает несколько связанных Task.

Mission не является Task.

Task — единица работы.

Mission — источник связанной работы.

Mission Run — экземпляр выполнения Mission.

Mission существует постоянно на протяжении крупной цели.

Mission Run существует во время конкретного запуска Mission и сохраняется в артефактах как запись authorization, параметров и результата запуска.

Одна Mission может иметь несколько Mission Run за время своей жизни.

Mission Mode не заменяет основной жизненный цикл продукта, не создаёт новую каноническую роль, не отменяет Source Of Work и не отменяет review-gates. Все реализации внутри Mission продолжают выполняться как обычные задачи через Planning, Implementation, Validation и связанные артефакты.

Mission не даёт права:

- менять vision;
- менять цели продукта;
- расширять roadmap;
- добавлять крупные функции вне roadmap;
- принимать продуктовые решения;
- менять продуктовую стратегию.

Если в Mission требуется продуктовое решение, Mission должна остановиться и передать вопрос Studio Director для маршрутизации к Product Owner или заказчику по `DECISION_AUTHORITY.md`.

---

# Уровни автономности Mission Mode

Каждый Mission Run обязан иметь явно указанный autonomy level до начала выполнения backlog items.

Autonomy level определяет, сколько работы Студия может выполнить за один Mission Run и когда она обязана остановиться.

Autonomy level фиксируется в Mission Run Authorization (`MISSION_RUN.md`) и контролируется Studio Director.

## Single-Step Mission

Single-Step Mission — самый строгий уровень автономности.

Один Mission Run выполняет только одну backlog item.

После завершения одной backlog item Mission обязана остановиться, даже если backlog содержит следующие готовые задачи.

Single-Step Mission подходит для:

- первого запуска новой Mission;
- рискованных изменений;
- проверки нового процесса;
- ситуаций, где нужен плотный контроль пользователя.

Single-Step Mission обязана остановиться, если:

- завершена одна backlog item;
- исчерпан любой обязательный budget из Typed Budget;
- достигнут milestone;
- сработал любой stop condition;
- требуется продуктовое, архитектурное или процессное решение вне полномочий текущей роли.

## Bounded Multi-Cycle Mission

Bounded Multi-Cycle Mission — ограниченный многоцикловый уровень автономности.

Один Mission Run может выполнить несколько backlog items подряд, если они находятся внутри Mission scope, имеют Source Of Work, сохраняют trace и проходят обычные validation gates.

Количество циклов ограничено заранее заданным Typed Budget.

Bounded Multi-Cycle Mission обязана остановиться, если:

- исчерпан любой обязательный budget из Typed Budget;
- завершён milestone;
- сработал stop condition;
- требуется продуктовое решение;
- следующая backlog item выходит за выбранный autonomy level или scope Mission.

Bounded Multi-Cycle Mission подходит для:

- стабильных roadmap stages;
- технического долга;
- тестового покрытия;
- последовательных задач с понятными зависимостями.

## Full Mission

Full Mission — максимальный уровень автономности Mission Mode.

Full Mission может работать до достижения всей цели Mission.

Full Mission допустима только для хорошо ограниченных Mission с низким риском.

Full Mission всё равно обязана соблюдать:

- Source Of Work;
- scope protection;
- stop conditions;
- validation gates;
- Typed Budget текущего Mission Run.

Full Mission не является режимом по умолчанию. На этапе v0.2 он описан как осторожный будущий режим и требует явного разрешения перед запуском.

---

# Typed Budget Model

Typed Budget Model описывает budget конкретного Mission Run.

Budget принадлежит Mission Run Authorization (`MISSION_RUN.md`), а не Mission Definition. Mission может задавать только mission-level guardrails: допустимый roadmap stage, общие ограничения, stop conditions и максимальные рамки для будущих запусков.

Каждый Mission Run обязан фиксировать budget в независимых категориях.

## Work Budget

Work Budget ограничивает объём выполняемой работы.

Примеры:

- max backlog items;
- max implementation cycles;
- max validation cycles;
- max review tasks, если review является частью запуска.

Work Budget обязателен для каждого Mission Run.

## Change Budget

Change Budget ограничивает объём изменений.

Примеры:

- max files changed;
- max repositories touched;
- max project implementation files changed;
- max mission artifact files changed, если это важно для запуска.

Change Budget обязателен для любого Mission Run, который может изменять файлы, артефакты или репозитории. Для strictly read-only или analysis-only запуска Change Budget может быть указан как `Not Applicable` с причиной.

## Scope Budget

Scope Budget ограничивает масштаб Mission Run.

Примеры:

- max roadmap stages;
- max milestones;
- max product areas;
- allowed milestone set.

Scope Budget обязателен для каждого Mission Run.

## Governance Budget

Governance Budget ограничивает длительность управленческого цикла.

Примеры:

- max mission reviews;
- max execution windows;
- max authorization renewals;
- time limit, если он нужен.

Governance Budget обязателен для каждого Mission Run. Конкретный time limit может отсутствовать, если запуск ограничен execution windows, mission reviews или другим измеримым governance limit.

## Budget Exhaustion

Studio Director проверяет Typed Budget:

- перед запуском Mission Run;
- перед выбором каждой следующей backlog item;
- после каждого Validation result;
- во время Mission Review;
- при любом событии, которое может изменить расход Work, Change, Scope или Governance Budget.

Исчерпание любого обязательного budget останавливает Mission Run.

Если optional budget не задан, он должен быть явно отмечен как `Not Applicable` в `MISSION_RUN.md`; отсутствие budget без объяснения считается неполной Authorization.

После остановки по budget Studio Director обязан обновить `MISSION_RUN.md`, зафиксировать stop reason и подготовить Mission Review перед дальнейшей реализацией.

## Повышение уровня автономности

Ни одна роль не может самостоятельно повышать уровень автономности активного Mission Run.

Single-Step Mission нельзя самовольно превратить в Bounded Multi-Cycle Mission.

Bounded Multi-Cycle Mission нельзя самовольно превратить в Full Mission.

Повышение autonomy level требует явного разрешения пользователя или Studio Director в рамках заранее заданных полномочий Mission.

Если требуемый уровень автономности не разрешён, Mission обязана остановиться и зафиксировать вопрос в Mission Review.

---

# Жизненный цикл Mission

Mission Mode использует следующий служебный lifecycle поверх Task Mode:

1. Mission Intake
2. Mission Planning
3. Backlog Generation
4. Mission Run Authorization
5. Implementation Loop
6. Mission Review
7. Mission Complete

Mission lifecycle не является заменой основного жизненного цикла продукта. Он управляет последовательностью связанных задач внутри уже подтверждённого Source Of Work, roadmap, review или другого допустимого источника.

## 1. Mission Intake

Пользователь или Studio Director фиксирует Mission.

Вход:

- репозиторий или проектный контекст;
- roadmap, review, решение или другой Source Of Work;
- ограничения Mission;
- критерии завершения;
- условия остановки.

Выход:

- Mission Definition в `MISSION.md`.

## 2. Mission Planning

Studio Director анализирует входные данные и определяет границы Mission.

Определяются:

- scope;
- milestones;
- ограничения;
- mission-level budget guardrails;
- stop conditions;
- критерии завершения.

Выход:

- Mission Plan в `MISSION.md`;
- начальное состояние в `MISSION_STATE.md`.

## 3. Backlog Generation

Delivery Planner создаёт Mission Backlog.

Все задачи должны ссылаться на Mission как Source Of Work и сохранять trace до исходного roadmap, review, backlog item или другого подтверждённого источника.

Обязательная цепочка trace:

```text
Mission → Roadmap / Review / Backlog Item → Task
```

Выход:

- `MISSION_BACKLOG.md`.

Task Specifications создаются после Mission Run Authorization и выбора backlog item для выполнения.

## 4. Mission Run Authorization

Mission Run Authorization создаёт конкретный запуск Mission.

Mission не может начать выполнение backlog items без `MISSION_RUN.md`.

Mission Run Authorization должен существовать между Mission и выбором backlog item для выполнения.

Обязательная цепочка запуска:

```text
Mission
↓
Mission Run Authorization
↓
Mission Review / Current Mission Status
↓
Backlog Item
```

Studio Director создаёт Mission Run Authorization и фиксирует:

- Mission Run ID;
- Mission ID;
- Autonomy Level;
- Allowed Scope;
- Typed Budget;
- Stop Conditions;
- Run Status;
- Created By;
- Created At.

Mission Run Authorization не заменяет Mission Definition. Mission Definition хранит цель, roadmap, границы и mission-level состояние. Mission Run Authorization хранит параметры конкретного запуска, typed budget, autonomy level, execution status and run result.

Выход:

- `MISSION_RUN.md`.

## 5. Implementation Loop

Для каждой задачи внутри Mission применяется обычный Task Mode:

- Delivery Planner формулирует задачу;
- Implementer выполняет задачу;
- Validator проводит проверку;
- Historian обновляет знания и артефакты, если результат должен сохраниться.

Задача закрывается только после обычной проверки качества. Mission Mode не отменяет Validation.

Выход:

- Implementation Reports;
- Validation Reports;
- обновлённые Mission State, Mission Backlog и Project Memory, если требуется.

## 5.1 Single-Step Autonomous Mission Loop

Single-Step Autonomous Mission Loop — строгий уровень автономности Mission Mode.

Один запуск Mission в Single-Step режиме может выполнить не больше одной backlog item.

Официальный цикл:

```text
Mission State
↓
Mission Run Authorization
↓
Mission Review
↓
Выбор следующей backlog item
↓
Delivery Planner
↓
Task Specification
↓
Implementer
↓
Validator
↓
Mission State Update
↓
Stop
```

Studio Director управляет циклом, но не реализует задачу сам.

Перед запуском Single-Step цикла Studio Director обязан:

- открыть Mission;
- создать или открыть `MISSION_RUN.md`;
- прочитать `MISSION_STATE.md`;
- прочитать последний `MISSION_REVIEW.md`;
- проверить, что Mission Run Authorization разрешает Single-Step Mission;
- определить следующую backlog item из `MISSION_BACKLOG.md`;
- проверить Typed Budget из Mission Run Authorization;
- проверить stop conditions из Mission Run Authorization и Mission Definition;
- проверить, что backlog item имеет Source Of Work и trace;
- назначить Delivery Planner для подготовки Task Specification.

После Validation Studio Director обязан:

- обновить `MISSION_STATE.md`;
- обновить статус backlog item в `MISSION_BACKLOG.md`;
- добавить Mission Execution Record в `MISSION_REVIEW.md`;
- зафиксировать новые риски, блокеры и Opportunities;
- остановить Mission.

Правило одного шага:

```text
one Mission run = one backlog item
```

После завершения одной backlog item Mission обязана остановиться даже если backlog содержит следующие задачи.

Single-Step Mission обязана остановиться, если:

- backlog item заблокирована;
- Validator отклонил результат;
- требуется решение Product Owner;
- исчерпан обязательный budget из Typed Budget;
- обнаружен архитектурный риск;
- сработал любой stop condition Mission.

Single-Step Loop не даёт права выполнять несколько задач подряд.

## 5.2 Bounded Multi-Cycle Mission Loop

Bounded Multi-Cycle Mission Loop позволяет одному Mission Run выполнить несколько backlog items подряд в пределах заранее заданного Typed Budget.

Официальный цикл повторяется для каждой выбранной backlog item:

```text
Mission State
↓
Mission Run Authorization
↓
Mission Review / Current Mission Status
↓
Выбор следующей backlog item
↓
Delivery Planner
↓
Task Specification
↓
Implementer
↓
Validator
↓
Mission State Update
↓
Typed Budget and Stop Condition Check
↓
Continue or Stop
```

Перед каждым следующим циклом Studio Director обязан проверить:

- Mission Run Authorization exists and is active;
- выбранный autonomy level в `MISSION_RUN.md`: Bounded Multi-Cycle Mission;
- оставшийся Typed Budget из `MISSION_RUN.md`;
- stop conditions из Mission Run Authorization и Mission Definition;
- достижение milestone;
- Source Of Work и trace следующей backlog item;
- что следующая backlog item не расширяет scope Mission.

Bounded Multi-Cycle Mission обязана остановиться при исчерпании любого обязательного budget, завершении milestone, stop condition или необходимости продуктового решения.

## 5.3 Full Mission Loop

Full Mission Loop может продолжаться до достижения всей цели Mission.

Full Mission не является режимом по умолчанию и не должен использоваться без явного разрешения.

Даже в Full Mission каждая задача выполняется через обычный Task Mode и проходит Validation.

Full Mission также требует `MISSION_RUN.md` с явным Autonomy Level: Full Mission, Allowed Scope, Typed Budget and Stop Conditions.

## 6. Mission Review

После каждого цикла или milestone Studio Director выполняет обзор Mission.

Проверяется:

- что сделано;
- какой Mission Run выполняется или завершён;
- какие риски появились;
- какие задачи остались;
- есть ли блокеры;
- достигнут ли milestone;
- не исчерпан ли обязательный budget из Typed Budget;
- не требуется ли продуктовое или архитектурное решение.

Выход:

- `MISSION_REVIEW.md`;
- обновлённый `MISSION_STATE.md`;
- обновлённый `MISSION_RUN.md`, если изменился статус запуска, использованный Typed Budget or stop reason;
- процессное решение: продолжить, остановить, завершить или эскалировать.

## 7. Mission Complete

Mission завершается, если:

- достигнут целевой milestone;
- выполнены критерии завершения;
- дальнейшая работа требует новой Mission;
- Mission остановлена по stop condition.

Выход:

- финальное состояние в `MISSION_STATE.md`;
- итоговый Mission Review;
- обновление Project Memory через Historian, если результат Mission имеет долговременное значение.

---

# Ограничения Mission Mode

Каждая Mission должна иметь:

- mission-level budget guardrails или указание, что concrete budget задаётся только в `MISSION_RUN.md`;
- stop conditions;
- критерии завершения;
- scope boundaries.

Concrete Typed Budget задаётся в Mission Run Authorization. Mission-level guardrails могут ограничивать допустимые максимумы для будущих запусков, но не заменяют Work, Change, Scope and Governance Budget конкретного Mission Run.

Mission обязана остановиться, если:

- требуется продуктовое решение;
- найден архитектурный блокер;
- roadmap противоречит проекту;
- есть несколько равноценных направлений развития;
- достигнут milestone;
- исчерпан любой обязательный budget текущего Mission Run.

Новые идеи, найденные во время Mission, фиксируются как Opportunity. Opportunity не расширяет Mission автоматически и требует решения Product Owner.

---

# Общая схема

```text
IDEA
↓
DISCOVERY
↓
PRODUCT DEFINITION
↓
SOLUTION DESIGN
↓
PLANNING
↓
IMPLEMENTATION
↓
VALIDATION
↓
RELEASE APPROVAL
↓
RELEASE
↓
PROJECT MEMORY UPDATE
```

---

# Ответственные роли и результаты

| Этап | Ответственная роль | Выход |
| --- | --- | --- |
| IDEA | Product Owner | Idea Brief |
| DISCOVERY | Product Analyst | Discovery Report |
| PRODUCT DEFINITION | Product Owner | Product Requirements Document (PRD) |
| SOLUTION DESIGN | Solution Architect | Architecture Document |
| PLANNING | Delivery Planner | Backlog и Task Specifications |
| IMPLEMENTATION | Implementer | Исходный код, автоматические тесты, Implementation Reports |
| VALIDATION | Validator | Validation Report |
| RELEASE APPROVAL | Studio Director при поддержке Release Manager | Approved, Approved With Conditions, Rework Required или Rejected |
| RELEASE | Release Manager | Release Package, включая Release Notes |
| PROJECT MEMORY UPDATE | Historian | Обновлённый Project Memory |

---

# Stage 1. Idea

## Цель

Получить первоначальную идею продукта от заказчика.

## Вход

Идея в любой форме:

- одно предложение;
- описание проблемы;
- список пожеланий;
- концепция продукта;
- набросок решения.

## Действия

- Зафиксировать идею.
- Определить область продукта.
- Создать первоначальный контекст проекта.

## Выход

- Idea Brief

## Критерий завершения

Идея зафиксирована и готова к исследованию.

---

# Stage 2. Discovery

## Цель

Понять проблему, предложенное решение, цели и ограничения.

## Действия

Студия задаёт уточняющие вопросы до получения достаточного контекста.

Вопросы должны относиться только к информации, влияющей на продуктовые или технические решения.

Запрещается собирать информацию без практической необходимости.

Если заказчик предложил конкретное решение, Студия анализирует, какую проблему оно должно решить и насколько оно связано с этой проблемой.

## Выход

- Discovery Report

## Критерий завершения

Студия понимает:

- какую проблему решает продукт;
- какое решение предложено заказчиком и как оно связано с проблемой;
- кто его пользователи;
- что считается успешным результатом;
- какие существуют ограничения;
- какие существуют риски и допущения.

Discovery Report достаточен для того, чтобы Product Owner мог начать создание PRD без дополнительных исследований.

---

# Stage 3. Product Definition

## Цель

Сформировать полное описание продукта.

## Действия

Студия определяет:

- цели продукта;
- бизнес-ценность;
- функциональные требования;
- пользовательские сценарии;
- критерии приёмки;
- нефункциональные требования.

## Выход

- Product Requirements Document (PRD)

## Критерий завершения

Существует достаточное описание продукта для начала проектирования решения без дополнительных продуктовых вопросов.

---

# Stage 4. Solution Design

## Цель

Спроектировать техническое решение.

## Действия

Студия:

- определяет архитектуру;
- выбирает технологии;
- определяет компоненты системы;
- выявляет риски;
- фиксирует архитектурные решения.

## Выход

- Architecture Document

## Критерий завершения

Существует технический план реализации продукта.

---

# Stage 5. Planning

## Цель

Подготовить реализацию.

## Действия

Студия:

- декомпозирует работу;
- определяет зависимости;
- определяет последовательность реализации;
- формирует план выполнения.

## Выход

- Backlog
- Task Specifications

## Критерий завершения

Все необходимые работы описаны и готовы к реализации.

---

# Stage 6. Implementation

## Цель

Создать программный продукт.

## Действия

Студия:

- реализует задачи;
- создаёт тесты;
- обновляет документацию;
- устраняет обнаруженные дефекты.

## Правила

Код без проверки качества считается незавершённым.

Реализация не считается завершённой до прохождения этапа Validation.

## Выход

- Исходный код
- Автоматические тесты
- Implementation Reports

## Критерий завершения

Все запланированные задачи реализованы.

---

# Stage 7. Validation

## Цель

Проверить качество результата.

## Действия

Студия выполняет:

- функциональное тестирование;
- интеграционное тестирование;
- регрессионное тестирование;
- архитектурную проверку;
- ревью кода;
- проверку соответствия требованиям.

## Правила

Агент не может самостоятельно принять собственную работу.

Проверка должна выполняться независимым агентом.

## Выход

- Validation Report

## Критерий завершения

Все обязательные проверки успешно завершены.

Критические дефекты отсутствуют.

---

# Stage 8. Release Approval

## Цель

Получить решение заказчика о готовности release candidate с точки зрения бизнес-требований.

Validation подтверждает качество.

Release Approval подтверждает соответствие бизнес-требованиям.

Release фиксирует результат.

Канонический процесс RELEASE APPROVAL определён в `RELEASE_APPROVAL.md`.

## Вход

- Validation Report
- PRD
- Release Candidate Summary
- Project State

## Действия

Studio Director при поддержке Release Manager предоставляет заказчику:

- перечень реализованных возможностей;
- перечень того, что не реализовано;
- результаты проверок;
- известные ограничения;
- известные риски;
- отклонения от первоначального плана;
- описание release candidate в формате, понятном без чтения технических артефактов целиком.

## Выход

Один из статусов:

- Approved
- Approved With Conditions
- Rework Required
- Rejected

## Критерий завершения

Получено решение заказчика и Studio Director определил следующий маршрут:

- переход в RELEASE;
- переход в RELEASE с условиями;
- возврат на нужный этап;
- фиксация отклонения без выпуска релиза.

---

# Stage 9. Release

## Цель

Зафиксировать релиз продукта.

RELEASE начинается только после RELEASE APPROVAL со статусом Approved или Approved With Conditions, если условия не требуют возврата на предыдущий этап.

## Действия

Студия:

- подготавливает релиз;
- обновляет документацию;
- фиксирует состояние проекта;
- создаёт релизные материалы.

## Выход

- Release Package, включая Release Notes

## Критерий завершения

Релиз официально сформирован и зафиксирован.

---

# Stage 10. Project Memory Update

## Цель

Сохранить знания проекта.

Project Memory Update является операцией обновления Project Memory, а не отдельным артефактом.

## Действия

Студия фиксирует:

- принятые решения;
- причины решений;
- отклонённые варианты;
- найденные проблемы;
- технические долги;
- накопленные знания;
- идеи для дальнейшего развития.

## Выход

- Обновлённый Project Memory

## Критерий завершения

Память проекта обновлена.

---

# Правило возврата

На любом этапе Студия может вернуть процесс на предыдущий этап.

Примеры:

- обнаружены противоречивые требования → возврат в Product Definition;
- обнаружена архитектурная проблема → возврат в Solution Design;
- обнаружены ошибки реализации → возврат в Implementation.

Каждый возврат должен содержать:

- причину возврата;
- последствия;
- рекомендуемые действия.

---

# Определение завершённости проекта

Проект считается завершённым только при выполнении всех условий:

1. Реализация завершена.
2. Проверки качества завершены.
3. Заказчик подтвердил соответствие бизнес-требованиям.
4. Релиз сформирован.
5. Память проекта обновлена.

До выполнения всех условий проект считается незавершённым.
