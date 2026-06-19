# Reconciliation Report
v0.1
2026-06-19

## Назначение

Этот документ фиксирует результат устранения архитектурных противоречий в документации AI Software Studio.

Цель reconciliation — привести роли, артефакты, жизненный цикл и инструкцию Studio Director к единой модели перед дальнейшей разработкой агентов.

## Найденные противоречия

### Разные названия ролей

`ARTIFACTS.md` использовал названия ролей, которых нет в канонической модели `AGENTS.md`:

- Product Agent;
- Business Analyst Agent;
- Product Manager Agent;
- Tech Lead Agent;
- Developer Agent;
- QA Agent;
- Project Historian Agent;
- Release Manager Agent.

### Несогласованные владельцы артефактов

Одни и те же зоны ответственности были описаны разными ролями:

- Discovery Report был связан с Product Owner, Product Analyst и Business Analyst Agent;
- PRD был связан с Product Owner, Product Analyst и Product Manager Agent;
- Backlog и Task Specification были связаны с Tech Lead Agent вместо Delivery Planner;
- Implementation Report был связан с Developer Agent вместо Implementer;
- Validation Report был связан с QA Agent вместо Validator;
- Project Memory был связан с Project Historian Agent вместо Historian.

### Release Notes

`LIFECYCLE.md` указывал Release Notes как выход этапа RELEASE, но `ARTIFACTS.md` не описывал такой артефакт.

### Project Memory Update

`LIFECYCLE.md` указывал Project Memory Update как выход этапа PROJECT MEMORY UPDATE, а `ARTIFACTS.md` описывал только Project Memory.

### Project State

Документация не содержала отдельного понятия для служебного состояния оркестратора. Из-за этого текущий этап, статус, назначенная роль, блокеры и последнее решение Studio Director не имели явного места в модели.

### Модель назначения агентов

Studio Director назначал "агентов" напрямую, но не было ясно, назначается каноническая роль или конкретный специализированный исполнитель.

## Принятые решения

### Канонические роли

Источником истины по ролям является `AGENTS.md`.

Финальный список ролей:

1. Studio Director
2. Product Owner
3. Product Analyst
4. Solution Architect
5. Delivery Planner
6. Implementer
7. Validator
8. Historian
9. Release Manager

Все владельцы артефактов приведены к этим названиям.

### Ответственность за продуктовые артефакты

Принята следующая модель:

- Product Owner создаёт Idea Brief и PRD;
- Product Analyst создаёт Discovery Report;
- Product Analyst может готовить аналитические разделы PRD по поручению Product Owner;
- владельцем PRD остаётся Product Owner.

Это сохраняет бизнес-ответственность Product Owner и аналитическую роль Product Analyst без дублирования владельцев.

### Ответственность за технические, плановые и проверочные артефакты

Принята следующая модель:

- Solution Architect создаёт Architecture Document;
- Delivery Planner создаёт Backlog и Task Specifications;
- Implementer создаёт исходный код, тесты и Implementation Reports;
- Validator создаёт Validation Report;
- Release Manager создаёт Release Package;
- Historian создаёт и обновляет Project Memory.

### Release Notes

Release Notes не выделяются в отдельный артефакт.

Release Notes являются разделом Release Package. Это снижает количество артефактов и сохраняет релизное описание в одном источнике истины.

### Project Memory Update

Project Memory является каноническим артефактом.

Project Memory Update является операцией обновления Project Memory, а не отдельным артефактом.

Этап PROJECT MEMORY UPDATE остаётся в жизненном цикле, но его выходом считается обновлённый Project Memory.

### Project State

Project State введён как служебное состояние оркестратора.

Project State не является продуктовым артефактом и не входит в канонический перечень артефактов проекта.

Владелец Project State: Studio Director.

Минимальный состав Project State:

- Current Stage
- Current Status
- Assigned Agent
- Active Artifacts
- Blocking Issues
- Escalation Status
- Last Decision

Project State используется Studio Director для маршрутизации работы, контроля переходов, фиксации блокеров и восстановления последнего процессного решения.

Project State не должен дублировать содержимое канонических артефактов.

### Назначение агентов

Studio Director назначает каноническую роль из `AGENTS.md`.

Если работу выполняет специализированный подагент или конкретный исполнитель, он считается исполнителем канонической роли.

Ответственность за результат остаётся за назначенной канонической ролью.

## Изменённые документы

### `documents/AGENTS.md`

Изменения:

- исправлена Markdown-структура дерева ролей;
- Studio Director описан как владелец Project State;
- Product Owner назначен владельцем Idea Brief и PRD;
- Product Analyst назначен владельцем Discovery Report;
- уточнено, что Product Analyst может готовить части PRD, но не владеет PRD;
- Release Package явно включает Release Notes;
- добавлено правило назначения канонических ролей и исполнителей ролей;
- Project State описан как служебное состояние, не заменяющее артефакты.

### `documents/ARTIFACTS.md`

Изменения:

- владельцы всех артефактов приведены к каноническим ролям из `AGENTS.md`;
- Release Notes добавлены как раздел Release Package;
- Project Memory Update описан как операция, а не отдельный артефакт;
- добавлено описание Project State как служебного объекта Studio Director.

### `documents/LIFECYCLE.md`

Изменения:

- добавлена таблица ответственных ролей и результатов по этапам;
- Release Notes включены в Release Package;
- выход этапа PROJECT MEMORY UPDATE изменён на обновлённый Project Memory;
- Project State описан как служебное состояние оркестратора, не являющееся этапом или артефактом.

### `documents/DECISION_AUTHORITY.md`

Изменения:

- процессные полномочия Studio Director дополнены назначением канонических ролей и исполнителей ролей;
- ведение Project State добавлено в область процессных решений Studio Director.

### `documents/agents/STUDIO_DIRECTOR.md`

Изменения:

- таблица жизненного цикла приведена к каноническим ролям;
- добавлено описание Project State;
- назначение агентов уточнено как назначение канонических ролей или исполнителей ролей;
- Release Notes включены в Release Package;
- Project Memory Update заменён на обновлённый Project Memory;
- удалён устаревший раздел Issues Found In Existing Documents.

### `documents/MANIFEST.md`

Изменения не требовались.

Философия, миссия, принципы автономности, качества, ответственности, прозрачности и памяти остались без изменений.

## Компромиссы

- Release Notes не стали отдельным артефактом, потому что отдельный артефакт увеличил бы бюрократию без явной пользы для текущей модели.
- Project Memory Update не стал отдельным артефактом, потому что Project Memory уже является каноническим источником истины для долговременной памяти.
- Project State не стал артефактом, чтобы не смешивать служебное состояние оркестратора с продуктовыми, техническими и релизными результатами.
- Product Analyst не стал владельцем PRD, чтобы сохранить Product Owner владельцем требований и бизнес-соответствия.
- В небольших проектах допускается один исполнитель на несколько ролей, но правило независимой проверки остаётся обязательным.

## Итоговая модель артефактов

Канонические артефакты:

1. Idea Brief
2. Discovery Report
3. Product Requirements Document (PRD)
4. Architecture Document
5. Backlog
6. Task Specification
7. Implementation Report
8. Validation Report
9. Release Package
10. Project Memory

Не являются отдельными артефактами:

- Release Notes — раздел Release Package;
- Project Memory Update — операция обновления Project Memory;
- Project State — служебное состояние Studio Director.

## Влияние на дальнейшую разработку агентов

- Все новые инструкции агентов должны использовать только канонические роли из `AGENTS.md`.
- Все новые артефакты должны иметь владельца из канонического списка ролей.
- Studio Director должен назначать роли, а не произвольные новые типы агентов.
- Подагенты допустимы как исполнители канонических ролей.
- Любое самостоятельное решение агента должно попадать в Project Memory через Historian.
- Текущее состояние оркестрации должно храниться в Project State и не должно дублировать содержимое артефактов.
