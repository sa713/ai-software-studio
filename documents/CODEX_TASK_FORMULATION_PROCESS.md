# CODEX_TASK_FORMULATION_PROCESS.md
v0.1
2026-06-22

## Назначение

Документ определяет, как AI Software Studio формулирует реализационные задачи для Codex.

Цель процесса — снять с заказчика обязанность вручную писать implementation prompts. Заказчик задаёт направление, ограничения или приоритет. Студия превращает этот вход в понятную, готовую к копированию задачу для Codex на основе roadmap, review findings, текущего состояния репозитория и правил Студии.

Документ не вводит новый lifecycle stage, новую роль или новый review-gate. Это handoff-процесс внутри Planning.

## Ответственный агент

За формулирование реализационных задач для Codex отвечает Delivery Planner.

Причины:

- `AGENTS.md` определяет Delivery Planner как владельца планирования реализации.
- `ARTIFACTS.md` определяет Backlog и Task Specification как артефакты Delivery Planner.
- Формулирование Codex-задачи — это planning handoff к Implementer, а не Discovery, Product Definition, Solution Design, Implementation или Validation.
- Product Analyst может дать продуктовый контекст, review findings и missing requirements, но не должен владеть декомпозицией работ.
- Product Owner владеет продуктом и PRD, но не должен становиться автором implementation tasks.
- Studio Director маршрутизирует процесс и назначает роль, но не пишет Task Specifications вместо Delivery Planner.

## Ответственность

Delivery Planner отвечает за:

- превращение roadmap в actionable backlog work;
- выбор следующей задачи;
- проверку и указание Source Of Work перед формулированием задачи;
- проверку зависимостей и текущего состояния репозитория перед выбором задачи;
- сохранение контекста из review reports, roadmap, Project State и выполненных implementation tasks;
- определение scope и out of scope;
- описание технических и продуктовых ограничений;
- указание вероятных файлов или зон проекта;
- формулирование acceptance criteria;
- формулирование ручной проверки;
- описание того, что Codex должен прислать на проверку;
- контроль, что задача достаточно мала для независимой реализации и проверки.

Delivery Planner не должен:

- быть источником новых инициатив;
- придумывать задачи без подтверждённого Source Of Work;
- менять продукт без решения Product Owner или заказчика;
- генерировать новые функции;
- менять roadmap по собственной инициативе;
- менять архитектуру без решения Solution Architect;
- писать код;
- валидировать собственную задачу как завершённую;
- обходить Validation или Release Approval.

## Source Of Work

Перед формулированием задачи Delivery Planner обязан указать Source Of Work.

Новая задача может появиться только из одного из следующих источников:

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

Обязательный формат раздела:

```markdown
## Source Of Work

- Source:
- Source Type:
- Source Reference:
- Trace:
```

Примеры:

- Source: Roadmap Stage 1
- Source: Review Finding #3
- Source: Validator Rework Request
- Source: Bug Report #12

Без указания Source Of Work задача считается некорректной.

Если Source Of Work отсутствует, Delivery Planner не должен формулировать задачу. Он должен вернуть запрос на уточнение или подготовить эскалацию через Studio Director.

## Входные данные

Перед формулированием Codex-задачи Delivery Planner проверяет доступный контекст.

Обязательные или предпочтительные входы:

- текущий roadmap или Recommended Roadmap;
- релевантный review report;
- активный Backlog или task list, если он есть;
- Project State или эквивалентный текущий статус;
- состояние репозитория и список изменённых файлов;
- результаты последних implementation tasks;
- ограничения от заказчика;
- текущая продуктовая цель и долгосрочное направление;
- релевантная архитектура или структура кода.

Если полного PRD, Architecture Document или Backlog нет, потому что проект развивается из Existing Project Review, Delivery Planner может использовать review report и roadmap как исходные источники. Это должно быть явно указано как допущение.

## Правила выбора задачи

Delivery Planner выбирает следующую Codex-задачу по правилам:

- соблюдать порядок roadmap и явные зависимости;
- снижать технический и продуктовый риск до добавления больших новых систем;
- отдавать приоритет testability, save safety, deterministic logic и читаемости до расширения баланса;
- не выбирать задачу, которая требует нерешённых продуктовых или архитектурных решений;
- держать каждую задачу независимо реализуемой и проверяемой;
- не объединять UI redesign, architecture refactoring и новые механики в одну задачу;
- если предыдущая работа затронула критичную shared logic, рассмотреть тесты или стабилизацию перед следующей функцией;
- если в репозитории есть незакоммиченные изменения, учитывать их как текущий контекст и явно фиксировать допущение.

Если два возможных следующих шага имеют разный продуктовый эффект, Delivery Planner должен передать вопрос через Studio Director к Product Owner или заказчику.

## Обязательный формат Codex-задачи

Все задачи для Codex формулируются в чистом Markdown.

Обязательные правила формата:

- одно цельное Markdown-сообщение;
- без code fence вокруг всего задания;
- без writing block;
- без HTML;
- без JSON;
- без псевдослайдов;
- без декоративной обвязки;
- так, чтобы заказчик мог сразу скопировать текст и вставить его в Codex;
- обычные Markdown-заголовки и списки разрешены;
- inline code разрешён для файлов, символов и команд;
- короткие примеры кода разрешены только если они действительно нужны для ясности реализации.

Задача должна содержать:

- название;
- Source Of Work;
- контекст;
- цель;
- scope;
- out of scope;
- требования;
- ограничения;
- вероятные файлы или зоны проекта;
- acceptance criteria;
- ручную проверку;
- список того, что Codex должен прислать на проверку.

## Quality Checklist

Перед передачей задачи Delivery Planner проверяет:

- у задачи есть один понятный результат;
- указан Source Of Work;
- Source Of Work относится к допустимым источникам;
- задача не меняет продуктовое направление;
- задача не меняет архитектуру;
- зависимости перечислены;
- исходный контекст назван;
- ограничения конкретны;
- acceptance criteria проверяемы;
- ручная проверка выполнима;
- requested return summary явно указан;
- задача не обёрнута в code block или другой не-Markdown формат.

## Применение: Idle Math Lab

Project: Idle Math Lab.

Проверенный контекст:

- `IDLE_MATH_LAB_REVIEW_AND_ROADMAP.md`;
- текущий список файлов репозитория;
- текущий `git status`;
- выполненный economy refactor: `EconomySnapshot.swift`, `EconomyCalculator.swift`;
- текущая persistence work: `GameSaveStore.swift`, `GameEngine.swift`, `project.pbxproj`;
- отсутствие XCTest target в текущем списке файлов.

Текущее допущение:

- EconomySnapshot и EconomyCalculator реализованы.
- GameSaveStore уже есть в working tree и должен считаться текущей технической основой после review/acceptance.
- XCTest target пока отсутствует.

Решение Delivery Planner:

Следующая Codex-задача — `Add XCTest Target for Pure Logic`.

Source Of Work:

- Source: `IDLE_MATH_LAB_REVIEW_AND_ROADMAP.md`, Stage 1, Task 3
- Source Type: review + roadmap
- Source Reference: Review findings about missing test target and testability risk; Development Roadmap Stage 1; `Task 3: Add XCTest Target for Pure Logic`
- Trace: Review found no XCTest target and weak pure-logic testability → Roadmap Stage 1 required adding XCTest target and base formula/migration tests → Delivery Planner selected next task after EconomySnapshot and GameSaveStore → Codex task `Add XCTest Target for Pure Logic`

Почему:

- roadmap явно ставит эту задачу после EconomySnapshot и GameSaveStore;
- последние изменения вынесли критичную экономику и persistence в pure или near-pure layers;
- перед Proof preview, Research readability и новыми formula/product systems нужно зафиксировать текущее поведение тестами;
- это снижает риск регрессий сохранений, формул и будущего баланса.

## Первая сформулированная Delivery Planner задача для Codex

# Task: Add XCTest Target for Pure Logic

## Source Of Work

- Source: `IDLE_MATH_LAB_REVIEW_AND_ROADMAP.md`, Stage 1, Task 3
- Source Type: review + roadmap
- Source Reference: Review findings about missing test target and testability risk; Development Roadmap Stage 1; `Task 3: Add XCTest Target for Pure Logic`
- Trace: Review → Roadmap → Delivery Planner → Task

## Контекст

В Idle Math Lab уже начата стабилизация основы игры:

- экономика вынесена в `EconomySnapshot.swift` и `EconomyCalculator.swift`;
- `GameEngine.swift` использует economy snapshot;
- Income Breakdown подключён к Formula Machine;
- persistence вынесен в `GameSaveStore.swift`;
- формат `GameState` не должен ломаться;
- следующий риск — отсутствие автоматических тестов для чистой игровой логики.

Работаем в папке `/Users/sa/Documents/codex/ios/Idle Math Lab`.

Задача должна стабилизировать уже существующую логику. Не добавлять новые игровые механики, не менять баланс, не менять UI.

## Цель

Добавить XCTest target для pure logic и покрыть первые критичные зоны:

- `EconomyCalculator`;
- `EconomySnapshot`;
- `GameSaveStore`;
- `GameState` decode/default behavior;
- `TheoremAllocation`;
- базовые research/project readiness helpers, если они уже доступны как чистая логика.

После задачи будущие изменения экономики, сохранений, Proof и research-прогресса должны проверяться быстрыми unit tests без запуска UI.

## Scope

1. Добавить unit test target `Idle Math LabTests` в Xcode project.
2. Подключить test target к существующему project/scheme так, чтобы `xcodebuild test` запускал тесты.
3. Добавить минимальные test helpers/fixtures для создания `GameState` без UI.
4. Добавить тесты для `EconomyCalculator`:
   - fresh state income snapshot;
   - tap income with current multipliers;
   - passive income with current upgrade tiers;
   - theorem multiplier;
   - focus multiplier;
   - paradigm multiplier;
   - active function multiplier;
   - theorem school multiplier;
   - cost discount;
   - compression overcap bonus;
   - proof reward preview.
5. Добавить тесты для `GameSaveStore`:
   - load without save returns fresh state;
   - save/load roundtrip preserves progress;
   - reset removes saved state;
   - corrupted save falls back to fresh state without crash;
   - legacy key `IdleMathLab.GameState.v1` is still supported.
6. Добавить тесты для `GameState` decoding compatibility where practical:
   - current encoded state decodes;
   - missing optional/newer fields keep safe defaults if current model supports that path.
7. Добавить тесты для `TheoremAllocation`:
   - unallocated theorem count is correct;
   - allocation cannot exceed available theorem budget through existing normalization/guards;
   - school values used by economy remain deterministic.
8. Добавить тесты для research/project readiness only if existing APIs allow it without UI or large refactor.
9. Если для тестирования `GameSaveStore` нужен injectable `UserDefaults`, добавить минимальный initializer, который по умолчанию сохраняет текущее поведение через `UserDefaults.standard`.

## Out Of Scope

Не делать:

- новый баланс;
- новые формулы дохода;
- новые исследования;
- новые апгрейды;
- новый UI;
- переработку Formula Machine;
- переработку GameEngine целиком;
- изменение структуры `GameState` без необходимости;
- изменение ключа сохранения без миграции;
- UI tests;
- snapshot tests;
- CI-настройку.

## Требования

- Тесты должны проверять текущее поведение, а не желаемый новый баланс.
- Production code можно менять только минимально для тестируемости.
- `EconomyCalculator` должен оставаться детерминированным.
- Тесты `GameSaveStore` не должны использовать реальный пользовательский `UserDefaults.standard`.
- Для persistence-тестов использовать отдельный `UserDefaults(suiteName:)` и очищать его после теста.
- Тесты не должны зависеть от текущей даты, сети, UI или порядка запуска.
- Существующие сохранения должны оставаться совместимыми.
- Приложение должно продолжать собираться как iOS app.

## Вероятные файлы

- `Idle Math Lab.xcodeproj/project.pbxproj`
- `Idle Math Lab.xcodeproj/xcshareddata/xcschemes/Idle Math Lab.xcscheme`
- `Idle Math LabTests/EconomyCalculatorTests.swift`
- `Idle Math LabTests/GameSaveStoreTests.swift`
- `Idle Math LabTests/GameStateTests.swift`
- `Idle Math LabTests/TheoremAllocationTests.swift`
- `Idle Math LabTests/ResearchProgressTests.swift`, только если тесты research readiness можно добавить без раздувания scope
- `Idle Math Lab/GameSaveStore.swift`, только если нужен injectable defaults

## Acceptance Criteria

- В проекте есть `Idle Math LabTests`.
- `xcodebuild test` запускает новый test target.
- Есть тесты на economy snapshot и ключевые multipliers.
- Есть тесты на save/load/reset/corrupted fallback/legacy key.
- Есть тесты на theorem allocation.
- Тесты не требуют SwiftUI screen rendering.
- Тесты не используют реальные пользовательские сохранения.
- Баланс игры не изменён.
- UI не изменён.
- `GameState` format не сломан.
- Existing app build проходит.
- Test run проходит локально.

## Ручная проверка

1. Запустить `xcodebuild -project "Idle Math Lab.xcodeproj" -scheme "Idle Math Lab" -destination 'platform=iOS Simulator,name=iPhone 16' CODE_SIGNING_ALLOWED=NO test`.
2. Запустить обычную сборку приложения.
3. Открыть игру в симуляторе.
4. Купить upgrade.
5. Закрыть и открыть приложение.
6. Проверить, что прогресс сохранился.
7. Выполнить Proof, если доступен.
8. Выполнить Debug Reset.
9. Перезапустить приложение и убедиться, что state fresh.

## Что прислать на проверку

1. Краткое описание решения.
2. Какие test target и test files добавлены.
3. Какие production files изменены и зачем.
4. Какие сценарии покрыты тестами.
5. Подтверждение, что тесты не трогают реальные сохранения.
6. Результат `xcodebuild test`.
7. Результат обычной сборки.
8. `git status --short`.

## Критерии готовности

Задача считается выполненной, если:

- XCTest target добавлен и запускается;
- pure logic тесты покрывают экономику, сохранения и theorem allocation;
- legacy save key проверен тестом;
- corrupted save fallback проверен тестом;
- тесты проходят стабильно;
- приложение собирается;
- текущий игровой цикл не изменён;
- задача не добавила новые механики и не изменила визуальный стиль.
