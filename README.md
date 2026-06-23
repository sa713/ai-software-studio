# AI Software Studio

AI Software Studio — автономная агентная студия разработки программного обеспечения. Она превращает идею заказчика в работающий программный продукт через управляемый жизненный цикл: исследование, UX design, определение продукта, game design для игровых проектов, проектирование, планирование, реализацию, проверку, релиз и обновление памяти проекта.

Студия решает задачу сокращения ручного управления разработкой: заказчик отвечает за бизнес-цель и принимает решения, влияющие на бизнес-результат, а агенты самостоятельно ведут продукт через процесс, принимая продуктовые, технические и процессные решения в пределах своих полномочий.

Основной принцип работы: каждый этап имеет владельца, результат фиксируется в каноническом артефакте, а контекст передаётся между агентами через документы и Project Memory, а не через устные договорённости.

Начиная с v2.1 Студия использует Operating Profiles: `Light`, `Standard` и `Deep`. Профиль не меняет роли и Source Of Work, но регулирует глубину lifecycle, объём артефактов, Mission reporting и Validation, чтобы малые задачи не проходили через полный тяжёлый процесс.

## Канонические документы

- [MANIFEST.md](documents/MANIFEST.md) — определяет миссию, главные принципы, границы ответственности заказчика и Студии, автономность, качество, прозрачность и память проекта.
- [LIFECYCLE.md](documents/LIFECYCLE.md) — задаёт единственный допустимый жизненный цикл продукта, этапы, ответственные роли, результаты и критерии перехода между этапами.
- [ARTIFACTS.md](documents/ARTIFACTS.md) — описывает канонические артефакты, их владельцев, назначение и то, для какой информации каждый артефакт является источником истины.
- [AGENTS.md](documents/AGENTS.md) — определяет канонические роли агентов, их ответственность, права, ограничения и правила взаимодействия.
- [DECISION_AUTHORITY.md](documents/DECISION_AUTHORITY.md) — определяет, какие решения принимает заказчик, какие принимает Студия, когда нужна эскалация и как разрешаются конфликты приоритетов.
- [OPERATING_PROFILES.md](documents/OPERATING_PROFILES.md) — определяет профили Light / Standard / Deep, compact artifacts, validation depth, Mission profiles, Product Owner Review Log и Mission Index.
- [PROJECT_STATE.md](documents/PROJECT_STATE.md) — определяет Project State как служебный объект оркестрации, его владельца, структуру, статусы и правила обновления.
- [RELEASE_APPROVAL.md](documents/RELEASE_APPROVAL.md) — определяет этап RELEASE APPROVAL, материалы согласования, решения заказчика и маршруты после приёмки.

## Агентная система

- **Studio Director** — главный оркестратор процесса. Управляет жизненным циклом, назначает роли, контролирует переходы между этапами и ведёт Project State.
- **Product Analyst** — отвечает за Discovery. Исследует идею, проблему, пользователей, ограничения, риски и готовит Discovery Report.
- **UX Designer** — отвечает за удобство использования. Формирует UX Requirements, UX Risks и выполняет UX Review с UX Findings.
- **Product Owner** — представляет продуктовую сторону внутри Студии. Фиксирует исходную идею и формирует PRD как источник истины для требований продукта.
- **Game Designer** — отвечает за качество игрового опыта в игровых проектах. Формирует Game Design Notes, Gameplay Risks, Gameplay Opportunities и выполняет Game Design Review с Gameplay Findings.
- **Solution Architect** — проектирует техническое решение. Отвечает за архитектуру, технологии, компоненты, технические риски и Architecture Document.
- **Delivery Planner** — подготавливает реализацию. Декомпозирует работу, определяет зависимости, порядок выполнения, Backlog и Task Specifications.
- **Implementer** — создаёт программный продукт. Пишет код, тесты, обновляет техническую документацию и фиксирует результаты в Implementation Reports.
- **Validator** — независимо проверяет качество результата. Сверяет реализацию с требованиями, архитектурой и критериями приёмки, затем выпускает Validation Report.
- **Historian** — поддерживает долговременную память проекта. Фиксирует решения, причины, альтернативы, технический долг, уроки и будущие идеи в Project Memory.
- **Release Manager** — оформляет релиз. Готовит Release Package, Release Notes, инструкции, сведения о составе релиза и известных ограничениях.

Подробные инструкции каждой роли находятся в [documents/agents/](documents/agents/).

## Порядок чтения документации

Официальный порядок изучения системы:

1. [MANIFEST.md](documents/MANIFEST.md)
2. [LIFECYCLE.md](documents/LIFECYCLE.md)
3. [ARTIFACTS.md](documents/ARTIFACTS.md)
4. [AGENTS.md](documents/AGENTS.md)
5. [DECISION_AUTHORITY.md](documents/DECISION_AUTHORITY.md)
6. [OPERATING_PROFILES.md](documents/OPERATING_PROFILES.md)
7. [PROJECT_STATE.md](documents/PROJECT_STATE.md)
8. [RELEASE_APPROVAL.md](documents/RELEASE_APPROVAL.md)
9. [инструкции агентов](documents/agents/)

Такой порядок идёт от общего смысла к исполнению. Сначала нужно понять, зачем существует Студия и какие принципы ей управляют. Затем — какой жизненный цикл она проходит, какие артефакты создаёт, какие роли за них отвечают, кто имеет право принимать решения и какой Operating Profile применим к работе. После этого стоит изучить Project State как модель оркестрации и Release Approval как модель приёмки заказчиком. Только затем имеет смысл читать инструкции отдельных агентов.

## Полный жизненный цикл

```text
Idea
→ Discovery
→ UX Design
→ Product Definition
→ Game Design (для игровых проектов)
→ Solution Design
→ Planning
→ Implementation
→ Validation
→ Release Approval
→ Release
→ Project Memory Update
```

Подробное описание этапов, ответственных ролей, результатов и критериев перехода находится в [LIFECYCLE.md](documents/LIFECYCLE.md).

## Как Студия работает с новой идеей

1. Заказчик формулирует идею в любой удобной форме.
2. Studio Director запускает процесс и назначает ответственную роль для текущего этапа.
3. Студия проходит жизненный цикл, создавая и обновляя канонические артефакты.
4. На этапе Release Approval заказчик принимает релиз или возвращает его на доработку.
5. После релиза Historian обновляет Project Memory, чтобы сохранить решения, контекст и накопленные знания.

## Структура репозитория

- [documents/](documents/) — канонические документы Студии: манифест, жизненный цикл, артефакты, роли, полномочия, Project State, Release Approval и сопутствующие отчёты.
- [documents/agents/](documents/agents/) — подробные инструкции канонических агентов.
- [documents/missions/MISSION_INDEX.md](documents/missions/MISSION_INDEX.md) — навигационный индекс миссий, если он создан для текущего состояния репозитория.
- `deploy_keys/` — служебная инфраструктурная директория для локального деплоя или публикации. Она не является частью канонической документации Студии.

## Что не является источником истины

README не является источником истины для правил Студии. Это навигационный документ и точка входа.

README не определяет жизненный цикл, структуру артефактов, роли, полномочия, Project State или правила Release Approval.

При конфликте между README и каноническими документами действует соответствующий канонический документ.

Приоритет документов, артефактов и решений определяется системой Студии, прежде всего правилами из [MANIFEST.md](documents/MANIFEST.md), [LIFECYCLE.md](documents/LIFECYCLE.md), [ARTIFACTS.md](documents/ARTIFACTS.md), [AGENTS.md](documents/AGENTS.md), [DECISION_AUTHORITY.md](documents/DECISION_AUTHORITY.md), [OPERATING_PROFILES.md](documents/OPERATING_PROFILES.md), [PROJECT_STATE.md](documents/PROJECT_STATE.md) и [RELEASE_APPROVAL.md](documents/RELEASE_APPROVAL.md).
