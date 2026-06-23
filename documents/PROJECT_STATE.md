# PROJECT_STATE.md
v0.3
2026-06-23

## Назначение

Project State — служебный объект оркестрации AI Software Studio.

Он фиксирует текущее состояние процесса: где находится проект в жизненном цикле, кто сейчас отвечает за работу, какие артефакты участвуют в текущем этапе, есть ли блокеры или эскалации и какое процессное решение было принято последним.

Project State нужен, чтобы Studio Director мог:

- маршрутизировать работу между ролями;
- контролировать переходы между этапами;
- фиксировать возвраты, блокировки и эскалации;
- восстанавливать последнее процессное решение;
- не терять состояние проекта между действиями агентов.

Project State решает проблему оркестрационного контекста. Он не хранит продуктовые знания, технические решения или результаты работы вместо канонических артефактов.

Project State не является продуктовым артефактом.

Project State является служебным объектом оркестрации.

---

# Отличие от артефактов проекта

Канонические артефакты содержат знания, решения и результаты работы проекта.

Project State содержит только состояние процесса.

Project State может ссылаться на артефакты, но не должен копировать их содержимое.

Например:

- PRD содержит требования продукта;
- Architecture Document содержит техническую архитектуру;
- Backlog содержит состав работ;
- Validation Report содержит результаты проверки;
- Project State содержит сведения о том, какой этап активен, какая роль назначена и какое процессное решение принято последним.

---

# Владелец

Владелец Project State — Studio Director.

Только Studio Director может изменять Project State.

Остальные роли могут читать Project State как источник текущего процессного состояния.

Остальные роли могут предлагать изменения Project State через результаты своей работы:

- артефакты;
- отчёты;
- findings;
- блокеры;
- рекомендации;
- запросы на возврат;
- запросы на эскалацию.

Предложение изменения не меняет Project State само по себе. Studio Director должен принять процессное решение и только после этого обновить Project State.

---

# Жизненный цикл Project State

## Создание

Project State создаётся Studio Director при запуске проекта или при первом получении идеи заказчика.

Начальное состояние должно зафиксировать:

- Project ID;
- Current Stage;
- Current Status;
- Current Objective;
- Assigned Role, если роль уже назначена;
- Assigned Executor, если назначен конкретный исполнитель;
- Active Artifacts, если они уже существуют;
- Blocking Issues;
- Escalation Status;
- Last Decision;
- Previous Decision;
- Last Updated.

## Обновление

Project State обновляется на протяжении всего жизненного цикла проекта.

Обновление Project State не является отдельным этапом жизненного цикла и не создаёт продуктовый артефакт.

Studio Director обязан обновить Project State при:

- создании Project State;
- смене этапа;
- назначении роли;
- назначении конкретного исполнителя;
- изменении текущей цели;
- завершении этапа;
- возврате на предыдущий этап;
- появлении блокера;
- устранении блокера;
- запуске эскалации;
- получении решения по эскалации;
- изменении статуса проекта;
- принятии процессного решения;
- закрытии проекта.

## Закрытие

Project State закрывается после завершения проекта по `LIFECYCLE.md`.

Проект считается завершённым, когда выполнены условия из `LIFECYCLE.md`: реализация завершена, проверки качества завершены, заказчик подтвердил соответствие бизнес-требованиям, релиз сформирован и Project Memory обновлён.

При закрытии Project State должен зафиксировать:

- `Current Stage: PROJECT MEMORY UPDATE`;
- `Current Status: Completed`;
- отсутствие активной назначенной роли, если работа завершена;
- отсутствие активных блокеров;
- отсутствие активной эскалации;
- последнее решение о завершении проекта;
- Last Updated.

Закрытый Project State может храниться для восстановления истории оркестрации, но не заменяет Project Memory.

---

# Связь с жизненным циклом

Project State отражает текущий этап из `LIFECYCLE.md`, но сам не является этапом жизненного цикла.

Project State не добавляет новые этапы.

Project State не меняет критерии перехода между этапами.

Project State фиксирует, какой этап активен, какое решение привело к этому состоянию и какая роль должна выполнить следующую работу.

Если активен Mission Mode, Project State может ссылаться на `MISSION.md`, `MISSION_STATE.md`, `MISSION_BACKLOG.md` и последний `MISSION_REVIEW.md` в `Active Artifacts`.

Project State не заменяет Mission State и не должен копировать содержимое `MISSION_STATE.md`. Mission State остаётся источником текущего состояния Mission, бюджета автономности, stop conditions и Mission-specific блокеров.

---

# Каноническая структура

Project State должен содержать следующие поля.

## Project ID

Уникальный идентификатор проекта.

Обязательное поле.

## Current Stage

Текущий этап жизненного цикла.

Обязательное поле.

Допустимые значения:

- `IDEA`
- `DISCOVERY`
- `UX DESIGN`
- `PRODUCT DEFINITION`
- `GAME DESIGN`
- `SOLUTION DESIGN`
- `PLANNING`
- `IMPLEMENTATION`
- `VALIDATION`
- `RELEASE APPROVAL`
- `RELEASE`
- `PROJECT MEMORY UPDATE`

Значения должны соответствовать `LIFECYCLE.md`.

## Current Status

Текущий процессный статус проекта или этапа.

Обязательное поле.

Допустимые значения:

- `Not Started` — процесс или этап ещё не начат.
- `In Progress` — работа по текущему этапу выполняется.
- `Waiting For Input` — работа ожидает входных данных или результата роли.
- `Waiting For Decision` — работа ожидает процессного решения Studio Director или решения владельца области.
- `Blocked` — дальнейшее продвижение невозможно без устранения блокера.
- `Completed` — текущий этап или проект завершён.
- `Returned` — процесс возвращён на предыдущий этап.
- `Escalated` — вопрос вынесен на эскалацию.

Эта модель намеренно короткая. Она покрывает оркестрационные состояния без превращения Project State в трекер задач или систему управления требованиями.

## Assigned Role

Каноническая роль, которая сейчас отвечает за выполнение следующей работы.

Обязательное поле, если есть активное назначение.

Допустимые значения соответствуют `AGENTS.md`:

- `Studio Director`
- `Product Analyst`
- `UX Designer`
- `Product Owner`
- `Game Designer`
- `Solution Architect`
- `Delivery Planner`
- `Implementer`
- `Validator`
- `Historian`
- `Release Manager`

Если активного назначения нет, поле должно содержать `None`.

## Assigned Executor

Конкретный исполнитель, выполняющий назначенную роль, если он отличается от канонической роли или если используется специализированный подагент.

Обязательное поле.

Если специализированный исполнитель не назначен, поле должно содержать `Same as Assigned Role` или `None`.

Примеры:

- `Python Implementer`;
- `React Implementer`;
- `Release Manager`;
- `None`.

Assigned Executor не создаёт новую каноническую роль и не меняет ответственность Assigned Role.

## Active Artifacts

Список артефактов, участвующих в текущем этапе.

Обязательное поле.

Project State хранит только ссылки, идентификаторы, пути, версии или статусы артефактов.

Project State не хранит содержимое артефактов.

Для каждого активного артефакта указываются:

- `Artifact`;
- `Path or Reference`;
- `Version`, если есть;
- `Owner`;
- `Status`;
- `Purpose In Current Stage`.

## Blocking Issues

Список блокеров, препятствующих продвижению процесса.

Обязательное поле.

Если блокеров нет, значение должно быть `None`.

Для каждого блокера обязательны поля:

- `ID`;
- `Description`;
- `Severity`;
- `Source`;
- `Created By`;
- `Recommended Action`.

Допустимые значения `Severity`:

- `Critical`;
- `Major`;
- `Minor`.

Блокер должен быть связан с процессным препятствием. Дефекты реализации, требования, архитектурные вопросы или риски должны оставаться в своих канонических артефактах и только ссылаться из Blocking Issues, если они блокируют процесс.

## Escalation Status

Текущий статус эскалации.

Обязательное поле.

Допустимые значения:

- `No Escalation` — активной эскалации нет.
- `Pending` — Studio Director подготовил эскалацию, но она ещё не передана или не оформлена полностью.
- `Waiting For Customer` — вопрос передан заказчику и ожидает ответа.
- `Resolved` — решение получено и зафиксировано.

Если `Escalation Status` не равен `No Escalation`, Project State должен содержать ссылку на вопрос, решение или связанный артефакт в `Last Decision`, `Blocking Issues` или `Active Artifacts`.

## Last Decision

Последнее процессное решение Studio Director.

Обязательное поле.

Структура:

- `Decision`;
- `Decision Maker`;
- `Date`;
- `Reason`;
- `Related Artifacts`.

`Decision Maker` обычно равен `Studio Director`. Если решение основано на ответе заказчика, это указывается в `Reason` и `Related Artifacts`, но обновление Project State всё равно выполняет Studio Director.

## Previous Decision

Предыдущее процессное решение Studio Director.

Обязательное поле.

Структура совпадает с `Last Decision`:

- `Decision`;
- `Decision Maker`;
- `Date`;
- `Reason`;
- `Related Artifacts`.

Если предыдущего решения нет, значение должно быть `None`.

Previous Decision нужен для восстановления изменения состояния без превращения Project State в полный журнал. Долгосрочная история решений хранится в Project Memory.

## Current Objective

Текущая процессная цель.

Обязательное поле.

Примеры:

- `Create Idea Brief from customer idea`;
- `Complete Discovery Report`;
- `Fix implementation defects found during Validation`;
- `Prepare Release Package after approval`.

Current Objective не должен содержать полный scope задачи, требования продукта или техническое решение. Для этого используются канонические артефакты.

## Last Updated

Дата и время последнего обновления Project State.

Обязательное поле.

Формат должен быть однозначным для проекта. Рекомендуемый формат: `YYYY-MM-DD HH:MM` с указанием часового пояса, если это важно для проекта.

---

# Правила обновления

Studio Director обязан обновлять Project State сразу после процессного решения.

## Смена этапа

При переходе на новый этап Studio Director обновляет:

- Current Stage;
- Current Status;
- Assigned Role;
- Assigned Executor;
- Active Artifacts;
- Current Objective;
- Previous Decision;
- Last Decision;
- Last Updated.

## Назначение роли

При назначении роли Studio Director обновляет:

- Assigned Role;
- Assigned Executor;
- Current Status;
- Current Objective;
- Last Decision;
- Last Updated.

## Завершение этапа

При завершении этапа Studio Director обновляет:

- Current Status;
- Active Artifacts;
- Blocking Issues;
- Escalation Status;
- Previous Decision;
- Last Decision;
- Last Updated.

Если следующий этап начинается сразу, Project State также обновляется по правилу смены этапа.

## Возврат

При возврате на предыдущий этап Studio Director обновляет:

- Current Stage;
- Current Status: `Returned`;
- Assigned Role;
- Assigned Executor;
- Active Artifacts;
- Blocking Issues, если причина возврата блокирует продвижение;
- Current Objective;
- Previous Decision;
- Last Decision;
- Last Updated.

Last Decision должен содержать целевой этап возврата, причину, последствия и связанные артефакты.

## Эскалация

При запуске эскалации Studio Director обновляет:

- Current Status: `Escalated` или `Waiting For Decision`;
- Escalation Status;
- Blocking Issues, если работа заблокирована до ответа;
- Last Decision;
- Last Updated.

При получении решения по эскалации Studio Director обновляет:

- Escalation Status: `Resolved`;
- Current Status;
- Blocking Issues;
- Active Artifacts, если решение повлияло на артефакты;
- Previous Decision;
- Last Decision;
- Last Updated.

## Блокировка проекта

При блокировке Studio Director обновляет:

- Current Status: `Blocked`;
- Blocking Issues;
- Last Decision;
- Last Updated.

## Разблокировка проекта

При устранении блокера Studio Director обновляет:

- Current Status;
- Blocking Issues;
- Last Decision;
- Last Updated.

Если блокер был связан с эскалацией, также обновляется Escalation Status.

## Закрытие проекта

При закрытии проекта Studio Director обновляет:

- Current Stage;
- Current Status;
- Assigned Role;
- Assigned Executor;
- Active Artifacts;
- Blocking Issues;
- Escalation Status;
- Current Objective;
- Previous Decision;
- Last Decision;
- Last Updated.

---

# Правила недублирования

Project State не хранит:

- требования;
- архитектуру;
- Backlog;
- Task Specifications;
- код;
- результаты тестов;
- содержимое Implementation Reports;
- содержимое Validation Reports;
- содержимое Release Package;
- содержимое Project Memory;
- полную историю решений.

Project State хранит только состояние процесса:

- текущий этап;
- текущий статус;
- назначение;
- ссылки на активные артефакты;
- блокеры;
- статус эскалации;
- последнее и предыдущее процессные решения;
- текущую цель;
- время последнего обновления.

---

# Использование ролями

## Studio Director

Studio Director создаёт, читает и изменяет Project State.

Он использует Project State для маршрутизации работы, контроля переходов, фиксации возвратов, блокеров и эскалаций.

## Product Analyst

Product Analyst читает Project State, чтобы понять текущий этап, назначение, активные артефакты, блокеры и процессное решение Studio Director.

Product Analyst может предложить обновление Project State через Discovery Report или сообщение Studio Director.

## UX Designer

UX Designer читает Project State, чтобы понять текущий этап, активные входные артефакты, scope UX Design или UX Review, блокеры и процессное решение Studio Director.

UX Designer может предложить обновление Project State через UX Requirements, UX Risks, UX Review, UX Findings или вопрос Studio Director.

## Product Owner

Product Owner читает Project State, чтобы понять текущий этап, активные входные артефакты, статус эскалации и процессные ограничения.

Product Owner может предложить обновление Project State через Idea Brief, PRD или вопрос Studio Director.

## Game Designer

Game Designer читает Project State, чтобы понять текущий этап, применимость GAME DESIGN, активные входные артефакты, scope Game Design или Game Design Review, блокеры и процессное решение Studio Director.

Game Designer может предложить обновление Project State через Game Design Notes, Gameplay Risks, Gameplay Opportunities, Game Design Review, Gameplay Findings или вопрос Studio Director.

## Solution Architect

Solution Architect читает Project State, чтобы понять назначение, текущую цель, активные артефакты и блокеры, влияющие на Solution Design.

Solution Architect может предложить возврат или эскалацию через Architecture Document или сообщение Studio Director.

## Delivery Planner

Delivery Planner читает Project State, чтобы понять текущую цель, активные PRD и Architecture Document, блокеры и решения Studio Director.

Delivery Planner может предложить возврат или эскалацию через Backlog, Task Specifications или сообщение Studio Director.

## Implementer

Implementer читает Project State, чтобы понять назначенную задачу, активные артефакты, текущий статус и блокеры.

Implementer может предложить обновление Project State через Implementation Report, блокер или запрос возврата.

## Validator

Validator читает Project State, чтобы понять Validation Scope, активные артефакты, текущие блокеры и последнее процессное решение.

Validator может предложить возврат, блокировку или переход вперёд через Validation Report.

## Historian

Historian читает Project State, чтобы понять последнее процессное решение, активные артефакты, эскалации, возвраты и блокеры, которые должны быть учтены в Project Memory.

Historian может предложить обновление Project State, если обнаружил противоречие, потерю контекста или проблему с Project Memory.

## Release Manager

Release Manager читает Project State, чтобы понять, разрешён ли Release, есть ли Release Approval, какие артефакты активны и есть ли блокеры выпуска.

Release Manager может предложить возврат или блокировку через Release Package или сообщение Studio Director.

---

# Примеры

## Новый проект: от идеи до начала Discovery

### Состояние 1. Идея получена

```yaml
Project ID: studio-example-001
Current Stage: IDEA
Current Status: In Progress
Assigned Role: Product Owner
Assigned Executor: Same as Assigned Role
Active Artifacts:
  - Artifact: Idea Brief
    Path or Reference: documents/projects/studio-example-001/idea_brief.md
    Version: v0.1
    Owner: Product Owner
    Status: Pending
    Purpose In Current Stage: Capture the initial customer idea
Blocking Issues: None
Escalation Status: No Escalation
Last Decision:
  Decision: Start project and assign Product Owner to create Idea Brief
  Decision Maker: Studio Director
  Date: 2026-06-19
  Reason: Customer provided a new idea
  Related Artifacts: None
Previous Decision: None
Current Objective: Create Idea Brief from customer idea
Last Updated: 2026-06-19 18:00 Europe/Moscow
```

### Состояние 2. Idea Brief создан, Discovery начинается

```yaml
Project ID: studio-example-001
Current Stage: DISCOVERY
Current Status: In Progress
Assigned Role: Product Analyst
Assigned Executor: Same as Assigned Role
Active Artifacts:
  - Artifact: Idea Brief
    Path or Reference: documents/projects/studio-example-001/idea_brief.md
    Version: v0.1
    Owner: Product Owner
    Status: Completed
    Purpose In Current Stage: Input for Discovery
  - Artifact: Discovery Report
    Path or Reference: documents/projects/studio-example-001/discovery_report.md
    Version: v0.1
    Owner: Product Analyst
    Status: Pending
    Purpose In Current Stage: Capture problem, users, constraints, risks and open questions
Blocking Issues: None
Escalation Status: No Escalation
Last Decision:
  Decision: Move from IDEA to DISCOVERY and assign Product Analyst
  Decision Maker: Studio Director
  Date: 2026-06-19
  Reason: Idea Brief exists and is ready for Discovery
  Related Artifacts:
    - documents/projects/studio-example-001/idea_brief.md
Previous Decision:
  Decision: Start project and assign Product Owner to create Idea Brief
  Decision Maker: Studio Director
  Date: 2026-06-19
  Reason: Customer provided a new idea
  Related Artifacts: None
Current Objective: Complete Discovery Report
Last Updated: 2026-06-19 18:30 Europe/Moscow
```

## Возврат: Validation → Implementation

### Состояние до возврата

```yaml
Project ID: studio-example-002
Current Stage: VALIDATION
Current Status: In Progress
Assigned Role: Validator
Assigned Executor: Same as Assigned Role
Active Artifacts:
  - Artifact: Implementation Report
    Path or Reference: documents/projects/studio-example-002/implementation_report_T-014.md
    Version: v0.1
    Owner: Implementer
    Status: Completed
    Purpose In Current Stage: Input for validation
  - Artifact: Validation Report
    Path or Reference: documents/projects/studio-example-002/validation_report_T-014.md
    Version: v0.1
    Owner: Validator
    Status: In Progress
    Purpose In Current Stage: Record validation findings
Blocking Issues: None
Escalation Status: No Escalation
Last Decision:
  Decision: Start Validation for task T-014
  Decision Maker: Studio Director
  Date: 2026-06-19
  Reason: Implementation Report was submitted
  Related Artifacts:
    - documents/projects/studio-example-002/implementation_report_T-014.md
Previous Decision:
  Decision: Complete Implementation for task T-014
  Decision Maker: Studio Director
  Date: 2026-06-19
  Reason: Implementer reported task ready for Validation
  Related Artifacts:
    - documents/projects/studio-example-002/implementation_report_T-014.md
Current Objective: Validate implementation for task T-014
Last Updated: 2026-06-19 19:00 Europe/Moscow
```

### Состояние после возврата

```yaml
Project ID: studio-example-002
Current Stage: IMPLEMENTATION
Current Status: Returned
Assigned Role: Implementer
Assigned Executor: Same as Assigned Role
Active Artifacts:
  - Artifact: Task Specification
    Path or Reference: documents/projects/studio-example-002/task_T-014.md
    Version: v0.1
    Owner: Delivery Planner
    Status: Active
    Purpose In Current Stage: Defines the required fix scope
  - Artifact: Validation Report
    Path or Reference: documents/projects/studio-example-002/validation_report_T-014.md
    Version: v0.1
    Owner: Validator
    Status: Failed
    Purpose In Current Stage: Source of defects to fix
  - Artifact: Implementation Report
    Path or Reference: documents/projects/studio-example-002/implementation_report_T-014.md
    Version: v0.1
    Owner: Implementer
    Status: Requires Update
    Purpose In Current Stage: Must be updated after fixes
Blocking Issues:
  - ID: BI-001
    Description: Validation found a failed mandatory Acceptance Criterion for task T-014
    Severity: Major
    Source: Validation Report T-014
    Created By: Validator
    Recommended Action: Return to Implementer to fix the failed criterion and update Implementation Report
Escalation Status: No Escalation
Last Decision:
  Decision: Return from VALIDATION to IMPLEMENTATION for task T-014
  Decision Maker: Studio Director
  Date: 2026-06-19
  Reason: Validation Report has status Failed due to a mandatory Acceptance Criterion
  Related Artifacts:
    - documents/projects/studio-example-002/validation_report_T-014.md
    - documents/projects/studio-example-002/task_T-014.md
Previous Decision:
  Decision: Start Validation for task T-014
  Decision Maker: Studio Director
  Date: 2026-06-19
  Reason: Implementation Report was submitted
  Related Artifacts:
    - documents/projects/studio-example-002/implementation_report_T-014.md
Current Objective: Fix defects found during Validation for task T-014
Last Updated: 2026-06-19 19:40 Europe/Moscow
```
