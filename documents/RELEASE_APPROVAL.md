# RELEASE_APPROVAL.md
v0.1
2026-06-19

## Назначение

RELEASE APPROVAL — этап жизненного цикла, на котором заказчик принимает решение о готовности release candidate с точки зрения бизнес-требований.

Этап существует, чтобы отделить независимую проверку качества от бизнес-приёмки и от последующей фиксации релиза.

Validation подтверждает качество.

Release Approval подтверждает соответствие бизнес-требованиям.

Release фиксирует результат.

Это три разные вещи:

- `VALIDATION` проверяет реализацию, требования, архитектуру, тесты, дефекты и риски.
- `RELEASE APPROVAL` показывает заказчику понятный состав release candidate и получает бизнес-решение.
- `RELEASE` оформляет утверждённый результат в Release Package.

RELEASE APPROVAL не является технической проверкой и не заменяет Validation.

RELEASE APPROVAL не является релизом и не заменяет Release Package.

---

# Владелец этапа

Владелец этапа — Studio Director.

Studio Director отвечает за:

- проверку готовности release candidate к согласованию;
- запуск этапа RELEASE APPROVAL;
- передачу заказчику понятных материалов;
- получение решения заказчика;
- фиксацию решения в Project State;
- выбор следующего маршрута жизненного цикла.

Release Manager обеспечивает подготовку материалов для согласования.

Заказчик принимает решение.

---

# Входные данные

Обязательные входы RELEASE APPROVAL:

- Validation Report;
- PRD;
- Release Candidate Summary;
- Project State.

Дополнительные входы при необходимости:

- Implementation Reports;
- Backlog;
- Task Specifications;
- Architecture Document;
- Project Memory;
- связанные решения Studio Director.

## Release Candidate Summary

Release Candidate Summary обязателен для RELEASE APPROVAL.

Release Candidate Summary не является отдельным каноническим артефактом проекта.

Причина: Release Candidate Summary является customer-facing материалом согласования, собранным из уже существующих источников истины. Если сделать его отдельным каноническим артефактом, появится риск дублирования PRD, Validation Report, Implementation Reports, Backlog и будущего Release Package.

Канонические источники остаются:

- PRD — требования продукта;
- Validation Report — результаты проверки качества;
- Implementation Reports — фактическая реализация;
- Backlog — состав работ;
- Project State — процессное состояние;
- Release Package — состояние утверждённого релиза после этапа RELEASE.

Release Candidate Summary используется только для принятия решения на RELEASE APPROVAL. После решения заказчика итог фиксируется в Project State, а релизное состояние фиксируется в Release Package на этапе RELEASE.

## Структура Release Candidate Summary

Release Candidate Summary должен быть кратким и понятным заказчику.

Обязательные разделы:

### Metadata

- Project ID;
- Prepared By: Release Manager;
- Reviewed By: Studio Director;
- Date;
- Source Artifacts.

### Release Candidate Scope

- что входит в release candidate;
- что не входит в release candidate;
- связь с требованиями PRD.

### Implemented Items

Для каждого элемента:

- название;
- пользовательский или бизнес-эффект;
- источник;
- ссылка на Validation.

### Not Implemented

Для каждого существенного не вошедшего пункта:

- пункт;
- причина;
- влияние;
- источник.

Если таких пунктов нет, раздел содержит `None`.

### Validation Summary

- Validation Status;
- краткий перечень выполненных проверок;
- Critical и Major defects, если есть;
- остаточные риски;
- ограничения проверки.

### Known Limitations

- ограничение;
- влияние на заказчика или пользователя;
- источник;
- требуется ли follow-up.

Если ограничений нет, раздел содержит `None`.

### Known Risks

- риск;
- возможное влияние;
- источник;
- recommendation.

Если рисков нет, раздел содержит `None`.

### Deviations From Plan

- отклонение;
- ожидаемое состояние;
- фактическое состояние;
- влияние;
- источник.

Если отклонений нет, раздел содержит `None`.

### Decision Request

- варианты решения заказчика;
- рекомендуемое решение Студии, если оно возможно;
- последствия каждого варианта.

---

# Что показывается заказчику

Заказчик не должен читать технические артефакты целиком.

Заказчику показывается Release Candidate Summary.

Минимальный состав информации:

- что реализовано;
- что не реализовано;
- насколько release candidate соответствует PRD;
- результаты Validation;
- известные ограничения;
- известные риски;
- отклонения от первоначального плана;
- что произойдёт при каждом варианте решения.

Технические артефакты должны быть доступны как источники, но не являются основным материалом для заказчика.

---

# Возможные решения заказчика

Допустимые решения:

- `Approved`;
- `Approved With Conditions`;
- `Rework Required`;
- `Rejected`.

Эта модель отделяет полное одобрение, условное одобрение, доработку и отказ от продолжения.

---

# Approved

`Approved` означает, что заказчик подтверждает соответствие release candidate бизнес-требованиям без дополнительных условий.

Последствия:

- Studio Director фиксирует решение в Project State;
- Studio Director переводит проект в `RELEASE`;
- Studio Director назначает Release Manager;
- Release Manager готовит Release Package;
- Historian позже фиксирует решение в Project Memory на этапе `PROJECT MEMORY UPDATE`.

Артефакты:

- Validation Report остаётся источником истины для качества;
- Release Candidate Summary остаётся материалом согласования;
- Release Package создаётся на этапе RELEASE.

---

# Approved With Conditions

`Approved With Conditions` означает, что заказчик принимает release candidate при выполнении явно указанных условий.

Допустимые условия:

- уточнить Release Notes без изменения смысла релиза;
- добавить инструкцию передачи результата;
- явно указать известное ограничение;
- зафиксировать follow-up после релиза;
- принять известный риск как допустимый;
- выполнить действие, которое находится в полномочиях Release Manager и не требует новой реализации или изменения требований.

Условие не должно:

- менять состав продукта;
- менять бизнес-цель;
- менять критерии приёмки;
- требовать новой реализации;
- требовать архитектурного изменения;
- скрывать Failed Validation;
- превращать неподтверждённую функциональность в часть релиза.

Если условие требует изменения продукта, архитектуры, реализации, критериев приёмки или повторной Validation, решение должно быть обработано как `Rework Required`, а не как `Approved With Conditions`.

Последствия допустимого `Approved With Conditions`:

- Studio Director фиксирует решение и условия в Project State;
- Studio Director переводит проект в `RELEASE`;
- Release Manager включает условия, ограничения и follow-up в Release Package;
- если условие должно быть сохранено долгосрочно, Historian фиксирует его в Project Memory на этапе `PROJECT MEMORY UPDATE`.

---

# Rework Required

`Rework Required` означает, что заказчик не принимает release candidate в текущем виде, но проект должен быть доработан.

Studio Director выбирает этап возврата.

Маршрут возврата определяется источником проблемы:

- изменение бизнес-цели, состава продукта, пользовательских ожиданий или критериев приёмки → `PRODUCT DEFINITION`;
- несоответствие требований и архитектуры → `SOLUTION DESIGN`;
- проблема планирования, scope задачи или декомпозиции → `PLANNING`;
- дефект реализации или неполная реализация → `IMPLEMENTATION`;
- недостаточная или спорная проверка → `VALIDATION`;
- непонятные материалы согласования → остаться на `RELEASE APPROVAL` и запросить доработку Release Candidate Summary у Release Manager.

Studio Director обязан:

- зафиксировать решение заказчика;
- определить причину отказа;
- определить целевой этап возврата;
- назначить ответственную роль;
- обновить Project State;
- указать, какие артефакты требуют обновления.

---

# Rejected

`Rejected` означает, что заказчик отклоняет release candidate или проектный результат и не запрашивает доработку в рамках текущего жизненного цикла.

Проект считается отклонённым, если заказчик явно сообщает, что:

- release candidate не должен выпускаться;
- доработка в рамках текущих целей не нужна;
- текущий результат не соответствует бизнес-ожиданиям настолько, что требуется остановка или новый проект;
- заказчик отказывается принимать результат и не выбирает маршрут rework.

Последствия:

- Studio Director не переводит проект в `RELEASE`;
- Studio Director фиксирует решение в Project State;
- Studio Director фиксирует причину отклонения и связанные материалы;
- если проект закрывается, Studio Director назначает Historian для обновления Project Memory;
- Release Package не создаётся как утверждённый релиз.

Rejected не является успешным завершением проекта.

Если заказчик после Rejected формулирует новую цель или новый продуктовый состав, это должно рассматриваться как новый запуск или возврат в более ранний этап по решению Studio Director.

---

# Обязанности Studio Director

Перед передачей release candidate заказчику Studio Director обязан проверить:

- этап `VALIDATION` завершён;
- Validation Report существует;
- Validation Status не равен `Failed`;
- PRD существует;
- Project State существует и отражает текущий этап;
- Release Candidate Summary подготовлен;
- состав согласования понятен;
- реализованные и нереализованные пункты различимы;
- известные ограничения и риски не скрыты;
- отклонения от плана указаны;
- заказчику не требуется читать технические артефакты целиком;
- варианты решения и последствия каждого варианта понятны.

Studio Director не должен отправлять release candidate на approval, если Validation Status равен `Failed`.

Studio Director не должен принимать решение за заказчика.

После решения заказчика Studio Director обязан:

- зафиксировать решение в Project State;
- обновить Current Status;
- обновить Last Decision и Previous Decision;
- обновить Active Artifacts;
- назначить следующую роль;
- выбрать следующий этап или этап возврата;
- обеспечить сохранение решения в Project Memory, если оно существенно для истории проекта.

---

# Обязанности Release Manager

Release Manager готовит материалы для согласования.

Release Manager обязан:

- подготовить Release Candidate Summary;
- извлечь customer-facing сведения из Validation Report, PRD, Implementation Reports и Backlog;
- показать, что реализовано;
- показать, что не реализовано;
- отразить Validation Status;
- отразить известные ограничения;
- отразить известные риски;
- отразить отклонения от плана;
- указать источники;
- сформулировать информацию понятным для заказчика языком;
- не скрывать ограничения, риски, Failed или Not Verifiable зоны;
- не включать неподтверждённую функциональность как готовую.

Release Manager не принимает решение за заказчика.

Release Manager не исправляет дефекты и не меняет реализацию в рамках RELEASE APPROVAL.

Если Release Manager обнаруживает, что материалы согласования требуют изменения продукта, архитектуры, реализации или Validation, он передаёт вопрос Studio Director.

---

# Правила эскалации

RELEASE APPROVAL является плановым бизнес-решением заказчика, а не исключительной технической эскалацией.

Вопрос считается бизнес-решением, если он влияет на:

- принятие результата заказчиком;
- соответствие бизнес-требованиям;
- состав продукта;
- пользовательские ожидания;
- критерии приёмки;
- готовность release candidate к выпуску с точки зрения заказчика.

Вопрос возвращается в обычный жизненный цикл, если он требует:

- изменения PRD;
- изменения Architecture Document;
- изменения Backlog или Task Specification;
- новой реализации;
- повторной Validation;
- исправления approval-материалов без бизнес-решения.

Технические вопросы не должны выноситься заказчику как часть RELEASE APPROVAL, если они не влияют на бизнес-результат или принятие релиза.

---

# Связь с Project State

При входе в RELEASE APPROVAL Studio Director обновляет Project State:

- `Current Stage: RELEASE APPROVAL`;
- `Current Status: Waiting For Decision` или `In Progress`;
- `Assigned Role: Studio Director`;
- `Assigned Executor`, если есть конкретный исполнитель;
- `Active Artifacts`: ссылки на Validation Report и PRD;
- `Last Decision.Related Artifacts`: ссылка на Release Candidate Summary как материал согласования и на связанные источники при необходимости;
- `Escalation Status: No Escalation`, если нет отдельной эскалации;
- `Current Objective: Obtain customer release approval`;
- `Last Decision`: решение о запуске RELEASE APPROVAL.

Release Approval не обязан переводить `Escalation Status` в `Waiting For Customer`, потому что это плановый этап приёмки, а не исключительная эскалация.

После решения заказчика Studio Director обновляет Project State:

- `Last Decision`;
- `Previous Decision`;
- `Current Status`;
- `Current Stage`;
- `Assigned Role`;
- `Assigned Executor`;
- `Active Artifacts`;
- `Blocking Issues`, если решение требует возврата;
- `Current Objective`;
- `Last Updated`.

---

# Примеры

## Approved

Ситуация:

- Validation Status: `Passed`;
- Release Candidate Summary показывает, что все обязательные требования PRD выполнены;
- известных блокирующих ограничений нет.

Решение заказчика:

- `Approved`.

Действия Studio Director:

- фиксирует `Approved` в Project State;
- переводит проект в `RELEASE`;
- назначает Release Manager;
- указывает Release Manager подготовить Release Package.

## Rework Required

Ситуация:

- Validation Status: `Passed With Risks`;
- заказчик видит, что важный пользовательский сценарий работает иначе, чем ожидалось;
- изменение влияет на пользовательские ожидания и критерии приёмки.

Решение заказчика:

- `Rework Required`.

Действия Studio Director:

- фиксирует решение в Project State;
- определяет, что проблема относится к Product Definition;
- возвращает проект в `PRODUCT DEFINITION`;
- назначает Product Owner;
- указывает обновить PRD или подготовить уточнение требований.

## Approved With Conditions

Ситуация:

- Validation Status: `Passed`;
- заказчик принимает release candidate, но просит явно указать в релизных материалах ограничение по развёртыванию и добавить follow-up после выпуска.

Решение заказчика:

- `Approved With Conditions`.

Условия:

- добавить ограничение в Release Notes;
- добавить follow-up item в Release Package.

Действия Studio Director:

- фиксирует решение и условия в Project State;
- переводит проект в `RELEASE`;
- назначает Release Manager;
- требует включить условия в Release Package.
