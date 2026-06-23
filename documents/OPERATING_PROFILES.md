# OPERATING_PROFILES.md
v0.1
2026-06-23

## Назначение

Документ определяет профили глубины работы AI Software Studio.

Цель профилей — снизить операционную стоимость Студии без потери Source Of Work, traceability, Typed Budget, независимой Validation и защиты от scope creep.

Operating Profile не создаёт новую роль, новый lifecycle stage или новый Source Of Work. Профиль определяет, насколько подробно должны выполняться уже существующие этапы, артефакты, Mission Mode и Validation.

## Канонические профили

Студия поддерживает три основных профиля:

- `Light`;
- `Standard`;
- `Deep`.

Дополнительный профиль `Specialized` используется только как уточнение к `Standard` или `Deep`, когда требуется UX Review, Game Design Review, security review, release review или другая специализированная проверка.

## Кто выбирает профиль

Studio Director выбирает Operating Profile перед началом работы или перед запуском Mission Run.

Studio Director обязан зафиксировать выбранный профиль в одном из мест:

- Project State;
- Task Specification;
- Mission Run Authorization;
- Mission Review, если профиль меняется во время Mission.

Если профиль не указан, действует `Standard`.

## Light

`Light` применяется для малых, локальных и низкорисковых работ.

Примеры:

- документационная правка;
- узкий bug fix;
- маленький script;
- локальный refactor без изменения поведения;
- простое изменение существующего процесса;
- small UI copy/layout adjustment без нового UX flow;
- изменение, не требующее новой архитектуры.

Минимальные требования:

- Source Of Work обязателен;
- scope и out of scope должны быть явно понятны;
- Task Specification может быть compact task card;
- Implementation Report может быть compact implementation note;
- Validation Report может быть Light Validation Report;
- Project Memory update необязателен, если решение не имеет долгосрочного значения;
- UX Design, Game Design, Discovery, PRD, Architecture Document и Release Package выполняются только если применимы к конкретной работе.

Запрещено использовать `Light`, если работа:

- меняет business goal, product promise, acceptance criteria или roadmap;
- создаёт новую feature с пользовательской ценностью;
- меняет архитектуру или публичный контракт;
- затрагивает security, privacy, payments, auth, migrations или production data;
- является крупной Mission;
- требует независимого UX Review или Game Design Review как условия качества.

## Standard

`Standard` применяется для обычной продуктовой или технической работы.

Примеры:

- feature в существующем продукте;
- обычный roadmap stage;
- изменение UX flow;
- изменение game system без высокого риска;
- техническое изменение с понятным blast radius;
- релизная подготовка.

Минимальные требования:

- Source Of Work обязателен;
- применимые lifecycle stages выполняются в обычном порядке;
- Task Specification, Implementation Report и Validation Report обязательны;
- PRD и Architecture Document обязательны для продуктовых или архитектурных изменений;
- UX artifacts обязательны для существенного UX surface;
- Game Design artifacts обязательны для существенного gameplay work;
- Project Memory обновляется после значимых решений, релиза, mission completion или изменения architecture/product direction.

## Deep

`Deep` применяется для high-risk, large-scope или стратегической работы.

Примеры:

- новый продукт;
- крупная Mission;
- security-sensitive работа;
- data migration;
- platform-level architecture change;
- существенный gameplay/system redesign;
- high-risk UX flow;
- release candidate for external users.

Минимальные требования:

- Source Of Work обязателен;
- применимые lifecycle stages выполняются в полном формате;
- full Task Specification, Implementation Report и Validation Report обязательны;
- Mission Mode должен иметь явный Mission Run Authorization и Typed Budget;
- Change Budget, Scope Budget и Governance Budget обязательны;
- Validation использует Deep или Specialized profile;
- Product Owner Review Log обязателен, если есть Opportunities, UX Findings или Gameplay Findings;
- Project Memory update обязателен после завершения.

## Specialized

`Specialized` не является самостоятельной заменой `Light`, `Standard` или `Deep`.

Он добавляется к выбранному профилю, если требуется специализированная проверка или экспертная область.

Примеры:

- `Standard + UX Review`;
- `Deep + Game Design Review`;
- `Deep + Security Review`;
- `Standard + Release Review`.

Specialized profile не даёт права обходить Product Owner Review, Source Of Work, Validation или Typed Budget.

## Artifact Weight Policy

Артефакты могут иметь две формы:

- `Full`;
- `Compact`.

`Full` используется в `Standard` и `Deep`, если артефакт является source of truth для продукта, архитектуры, релиза или Mission governance.

`Compact` разрешён в `Light` и documentation-only work, если сохраняются:

- Source Of Work;
- владелец;
- changed scope;
- decision or result;
- validation evidence;
- links to affected artifacts.

Compact form не должен скрывать решения, риски, assumptions, findings или changes of scope.

## Mission Mode Profiles

Mission Mode поддерживает три operating формы:

- `Mission Light`;
- `Mission Standard`;
- `Mission Deep`.

### Mission Light

Применяется для short documentation-only или process-cleanup missions.

Требуется:

- `MISSION.md`;
- `MISSION_RUN.md`;
- compact `MISSION_STATE.md`;
- compact `MISSION_REVIEW.md`;
- Mission Backlog как короткий список tasks or checklist.

Task-specific implementation and validation reports могут быть compact notes внутри Mission Review, если Mission Run Authorization явно разрешает compact reporting и сохраняет Source Of Work, changed files, validation evidence and stop-condition review.

### Mission Standard

Применяется для обычных roadmap or integration missions.

Требуется:

- `MISSION.md`;
- `MISSION_STATE.md`;
- `MISSION_BACKLOG.md`;
- `MISSION_RUN.md`;
- `MISSION_REVIEW.md`;
- Task Specifications;
- Implementation Reports;
- Validation Reports.

### Mission Deep

Применяется для high-risk, product-changing, security-sensitive или large-scope missions.

Требуется всё из `Mission Standard`, а также:

- detailed Typed Budget accounting;
- explicit stop reason review;
- Product Owner Review Log, если есть product-affecting findings or opportunities;
- Project Memory update после завершения.

## Validation Profiles

Validation всегда остаётся независимой.

Validator выбирает глубину проверки по назначенному Operating Profile:

- `Light Validation`;
- `Standard Validation`;
- `Deep Validation`;
- `Specialized Validation`.

### Light Validation

Проверяет:

- соответствие Source Of Work;
- соответствие scope;
- отсутствие очевидных regressions;
- наличие validation evidence;
- отсутствие несанкционированных изменений.

Light Validation может быть compact report, но должна явно указать verdict.

### Standard Validation

Проверяет:

- compliance with Task Specification;
- acceptance criteria;
- architecture constraints;
- tests or manual verification;
- implementation quality;
- risks and findings.

### Deep Validation

Проверяет всё из `Standard`, а также:

- broader regression risk;
- security, privacy or data risk, если применимо;
- maintainability and scalability;
- dependency risk;
- release readiness;
- remaining known risks.

### Specialized Validation

Используется, если обычная Validation должна учитывать отдельную expert area.

Validator не заменяет UX Designer, Game Designer или Solution Architect. Если нужна независимая UX или gameplay оценка, Validator фиксирует limitation и рекомендует Studio Director назначить соответствующую роль.

## Product Owner Review Log

Product Owner Review Log — лёгкий decision log для Opportunities, UX Findings и Gameplay Findings.

Он не является новой ролью и не заменяет PRD, Backlog или Mission Review.

Log может существовать как:

- раздел в PRD;
- раздел в Backlog;
- раздел в Mission Review;
- отдельный файл `PRODUCT_OWNER_REVIEW_LOG.md`, если очередь решений стала большой.

Каждая запись должна содержать:

- `Review Item ID`;
- `Source`;
- `Source Type`;
- `Source Reference`;
- `Trace`;
- `Decision: Approved, Rejected, Deferred, Needs Customer Decision`;
- `Decision Reason`;
- `Resulting Source Of Work`, если применимо;
- `Owner`;
- `Date`.

Product Owner Review Log нужен, чтобы Product Owner не становился неформальным bottleneck и чтобы findings не попадали в Backlog без trace.

## Mission Index

Mission Index — навигационный список активных, завершённых и архивированных миссий.

Mission Index не является source of truth для содержания Mission. Он хранит только pointers and statuses.

Рекомендуемое расположение:

```text
documents/missions/MISSION_INDEX.md
```

Минимальные поля:

- `Mission ID`;
- `Status`;
- `Operating Profile`;
- `Last Run`;
- `Current Decision`;
- `Primary Source Of Work`;
- `Mission Path`;
- `Review Path`;
- `Archive Status`.

Mission Index должен обновляться при создании, завершении или архивировании Mission.

## Archive Policy

Завершённые Mission не должны оставаться активным operating context.

После Mission Complete Studio Director должен:

- обновить Mission Index;
- оставить Mission artifacts как historical evidence;
- перенести долгосрочно важные решения в Project Memory, если применимо;
- не переписывать исторические mission artifacts без отдельного Source Of Work.

Historical reports, integration reviews and old roadmaps may remain as evidence, but active process must use current canonical docs and Mission Index.

## Stop Conditions

Operating Profile не отменяет stop conditions.

Работа должна остановиться, если:

- выбранный профиль недостаточен для фактического риска;
- Source Of Work отсутствует или не подтверждён;
- нужно Product Owner decision;
- требуется изменение roadmap, business goal, product promise or acceptance criteria;
- возникает architecture blocker;
- Validation требует глубины выше выбранного profile;
- Mission Run исчерпал Typed Budget.

Studio Director должен повысить профиль или подготовить эскалацию, если Light/Standard перестал соответствовать риску работы.
