# EXISTING_PROJECT_REVIEW.md
v0.2
2026-06-22

## Назначение

Existing Project Review — отдельный режим работы AI Software Studio для анализа уже существующих программных систем.

Режим принимает существующий проект и выдаёт структурированный результат аудита: проблемы, риски, улучшения и рекомендуемый план развития.

Existing Project Review не является новым жизненным циклом разработки.

Existing Project Review не заменяет `LIFECYCLE.md`.

Existing Project Review не добавляет этапы в основной процесс разработки.

Existing Project Review не создаёт новую роль.

---

# Цель режима

Цель Existing Project Review — помочь заказчику понять текущее состояние существующей системы и определить, что стоит улучшить.

Режим отвечает на вопросы:

- какие продуктовые проблемы или пропущенные сценарии есть в текущей системе;
- какие архитектурные риски и ограничения уже существуют;
- насколько качественно реализовано текущее решение;
- какие риски есть для эксплуатации, поддержки и развития;
- какие улучшения дадут наибольший эффект;
- какой roadmap развития разумно предложить.

Режим не отвечает на вопросы:

- какой новый продукт нужно создать с нуля;
- какие требования должны войти в PRD нового проекта;
- какой релиз нужно принять;
- какой код нужно немедленно переписать;
- какой новый lifecycle должен заменить основной процесс.

---

# Когда используется

Existing Project Review используется, когда входом является уже существующая система или её часть.

Примеры:

- ревью Telegram-бота;
- ревью мобильного приложения;
- ревью веб-приложения;
- ревью AI-агента;
- ревью внутреннего инструмента;
- ревью существующего GitHub-репозитория;
- ревью прототипа, который уже содержит код или рабочую реализацию;
- ревью legacy-проекта перед развитием;
- ревью проекта перед планированием рефакторинга или стабилизации.

Режим можно применять до запуска нового development lifecycle, после завершения проекта, либо отдельно от разработки как самостоятельную услугу анализа.

---

# Входные данные

Входом может быть один источник или комбинация источников:

- GitHub-репозиторий;
- исходный код;
- документация;
- архитектурные документы;
- описание существующей системы;
- README, инструкции запуска, deploy notes;
- issue tracker, backlog или список известных проблем;
- пользовательские сценарии;
- эксплуатационные заметки;
- результаты тестов или CI;
- Project Memory, если проект уже проходил через Студию.

Минимальное обязательное условие запуска аудита — хотя бы один источник анализа.

Обязательные входные данные:

- хотя бы один источник анализа.

Необязательные входные данные:

- документация;
- архитектурные документы;
- доступ к запуску;
- тестовые данные;
- инфраструктура.

Если входных данных недостаточно, Studio Director определяет, можно ли продолжать с ограничениями или нужно запросить недостающие материалы.

Отсутствие части входных данных должно быть явно зафиксировано как limitation или risk в Existing Project Review Report.

---

# Audit Intake Brief

Existing Project Review начинается с Audit Intake Brief.

Audit Intake Brief фиксирует:

- Project Name;
- Audit Goal;
- Audit Scope;
- Available Inputs;
- Missing Inputs;
- Audit Limitations;
- Requested Depth;
- Requested Deliverables.

Studio Director не должен запускать роли на аудит, пока цель, scope, доступные источники, ограничения и запрошенная глубина не зафиксированы в Audit Intake Brief или эквивалентном процессном решении.

Если заказчик передал только один источник анализа, например репозиторий или архив с кодом, аудит может начаться, но ограничения должны быть явно указаны.

---

# Review Depth

Existing Project Review поддерживает три уровня глубины.

## Light Review

Быстрый обзор для первичного понимания состояния проекта.

Используется, когда нужно быстро увидеть основные риски, грубые проблемы и очевидные направления улучшения.

Light Review не должен выдавать себя за полный аудит.

## Standard Review

Полноценный аудит по доступным входным данным.

Используется как уровень по умолчанию, если заказчик не указал другую глубину.

Standard Review должен покрывать Product Review, Architecture Review и Quality Review, если эти области применимы к scope.

## Deep Review

Максимально возможный анализ в рамках доступов, времени и scope.

Используется, когда нужно глубже проверить архитектурные решения, качество реализации, тестирование, эксплуатационные риски и долгосрочную сопровождаемость.

Deep Review всё равно ограничен доступными источниками и не превращается в pentest, performance audit, UX research или перепроектирование системы без отдельного решения Studio Director.

---

# Static-only Review

Static-only Review применяется, когда код или документы доступны, но запуск системы невозможен.

В таком режиме разрешено анализировать:

- структуру проекта;
- исходный код;
- зависимости;
- конфигурацию;
- тесты;
- документацию;
- архитектурные признаки;
- очевидные product gaps, если они видны из доступного контекста.

В Static-only Review нельзя достоверно подтвердить:

- фактическое runtime-поведение;
- работоспособность интеграций;
- производительность под нагрузкой;
- корректность deployment;
- реальное состояние инфраструктуры;
- пользовательский UX в рабочей среде;
- прохождение сценариев, которые требуют данных, секретов или внешних сервисов.

Все выводы, зависящие от запуска, должны быть отмечены как limitation, assumption, risk или follow-up.

Static-only Review может выявлять Defects, Risks и Improvements, но не должен утверждать, что система полностью работает или полностью не работает, если это невозможно проверить без запуска.

---

# Маршрут режима

Existing Project Review проходит как отдельный режим:

```text
Existing Project
↓
Audit
↓
Review
↓
Improvement Proposal
```

Этот маршрут не является заменой основного lifecycle:

```text
Idea
↓
Discovery
↓
Product Definition
↓
Solution Design
↓
Planning
↓
Implementation
↓
Validation
↓
Release Approval
↓
Release
↓
Project Memory Update
```

Existing Project Review может завершиться рекомендацией запустить основной lifecycle для нового развития, но сам по себе не создаёт PRD, Backlog, Task Specifications или Release Package.

---

# Оркестрация

Studio Director запускает Existing Project Review, если заказчик или процесс Студии явно просит оценить существующий проект.

Studio Director отвечает за:

- создание или принятие Audit Intake Brief;
- фиксацию цели review;
- определение review scope;
- определение входных источников;
- фиксацию missing inputs и audit limitations;
- определение requested depth;
- определение requested deliverables;
- назначение существующих ролей;
- сбор итогового Existing Project Review Report;
- принятие процессного решения после отчёта.

Project State не получает новых lifecycle stages для Existing Project Review. Если Studio Director должен отслеживать работу, он фиксирует её как отдельный review context или process decision, не меняя список этапов из `LIFECYCLE.md`.

---

# Роли

Existing Project Review использует только существующие роли.

## Product Analyst

Product Analyst анализирует продуктовую сторону существующей системы.

Он отвечает за:

- понимание текущей продуктовой цели;
- анализ известных пользователей и ролей;
- выявление отсутствующих пользовательских сценариев;
- выявление отсутствующих административных и операционных процессов;
- выявление отсутствующих процессов поддержки и сопровождения;
- выявление рисков эксплуатации;
- выявление противоречий между текущим решением и реальной проблемой;
- подготовку выводов для раздела `Product Review`.

Product Analyst не создаёт PRD в рамках Existing Project Review.

## Solution Architect

Solution Architect анализирует архитектуру и технические решения существующей системы.

Он отвечает за:

- анализ структуры системы;
- анализ компонентов и границ ответственности;
- анализ зависимостей и интеграций;
- анализ архитектурных решений;
- выявление архитектурного долга;
- выявление рисков масштабирования, сопровождения и эксплуатации;
- подготовку выводов для раздела `Architecture Review`.

Solution Architect не обязан перепроектировать систему в рамках Existing Project Review.

Если требуется новая архитектура, это фиксируется как recommendation или roadmap item.

## Validator

Validator применяет `CODE_REVIEW_FRAMEWORK.md` и выполняет экспертную оценку качества.

Он отвечает за:

- Architecture Review в части качества реализации;
- Code Quality Review;
- Security Review;
- Maintainability Review;
- Dependency Review;
- Test Coverage Review;
- классификацию findings как Defect, Risk, Improvement или Subjective Preference;
- отделение обязательных проблем от возможностей улучшения;
- подготовку выводов для раздела `Quality Review`.

Validator не исправляет код и не превращает review в обязательную переделку проекта.

---

# Границы ответственности Solution Architect и Validator

Solution Architect и Validator могут смотреть на одни и те же технические области, но отвечают на разные вопросы.

Solution Architect отвечает на вопросы:

- какая архитектура у существующей системы;
- какие архитектурные решения и ограничения видны;
- где границы компонентов, зависимостей и интеграций;
- какие архитектурные риски мешают развитию, масштабированию, сопровождению или эксплуатации;
- какие архитектурные изменения стоит рассмотреть как roadmap item.

Validator отвечает на вопросы:

- насколько качественно реализовано текущее решение;
- какие findings видны по критериям `CODE_REVIEW_FRAMEWORK.md`;
- какие проблемы являются Defect, Risk, Improvement или Subjective Preference;
- какие quality issues подтверждаются evidence;
- какие ограничения проверки мешают сделать более сильный вывод.

Если один и тот же вопрос затрагивает архитектуру и качество реализации, Solution Architect фиксирует design-level observation и архитектурные последствия, а Validator фиксирует implementation-quality finding, evidence и тип finding.

Validator не заменяет Solution Architect и не перепроектирует систему задним числом.

Solution Architect не заменяет Validator и не классифицирует quality findings вместо него.

---

# Артефакт режима

Обязательный стартовый артефакт режима — Audit Intake Brief.

Единственный обязательный итоговый артефакт режима — Existing Project Review Report.

Existing Project Review Report является источником истины для:

- выводов аудита существующего проекта;
- продуктовых проблем и blind spots;
- архитектурных рисков;
- quality findings;
- рисков эксплуатации, поддержки и развития;
- возможностей улучшения;
- recommended roadmap.

Existing Project Review Report не заменяет PRD, Architecture Document, Backlog, Validation Report, Release Package или Project Memory.

Если после review начинается разработка, новые артефакты основного lifecycle создаются отдельно по правилам `LIFECYCLE.md` и `ARTIFACTS.md`.

---

# Структура Existing Project Review Report

Обязательные разделы:

- Executive Summary;
- Product Review;
- Architecture Review;
- Quality Review;
- Risks;
- Improvement Opportunities;
- Recommended Roadmap.

Report должен ссылаться на Audit Intake Brief и сохранять выбранные Audit Scope, Requested Depth, Source Inputs и Limitations.

Каждый вывод в разделах Product Review, Architecture Review, Quality Review, Risks и Improvement Opportunities должен содержать:

- Observation — что обнаружено;
- Consequence — почему это важно и какие последствия;
- Recommendation — что рекомендуется сделать.

Report должен быть компактным и decision-oriented.

Report не должен превращаться в простыню текста, полный пересказ кода или список мелких вкусовых замечаний.

---

# Правила Findings

Existing Project Review использует модель findings из `CODE_REVIEW_FRAMEWORK.md`:

- Defect;
- Risk;
- Improvement;
- Subjective Preference.

Defect — проверяемая проблема, которая нарушает требование, корректность, безопасность, архитектурное ограничение, стабильность, сопровождаемость или ожидаемое поведение.

Risk — проблема или неопределённость, которая может повлиять на эксплуатацию, масштабирование, безопасность, поддержку, развитие или стоимость изменений.

Improvement — полезное улучшение, которое не является обязательным исправлением.

Subjective Preference — вкусовое или стилевое замечание без доказанного влияния на качество, риски или сопровождение.

Subjective Preference не должна попадать в Recommended Roadmap как обязательный пункт.

---

# Recommended Roadmap

Recommended Roadmap — предложение развития существующей системы.

Roadmap должен группировать работу по смыслу и приоритету:

- Critical Fixes;
- Risk Reduction;
- Product Gaps;
- Architecture Improvements;
- Quality Improvements;
- Operational Improvements;
- Later Opportunities.

Recommended Roadmap не является Backlog.

Recommended Roadmap не создаёт обязательства реализации.

Если заказчик решает реализовывать roadmap, Studio Director запускает соответствующий маршрут основного lifecycle или отдельное процессное решение.

---

# Ограничения

Existing Project Review не должен:

- создавать новую роль;
- создавать Project Auditor;
- менять `LIFECYCLE.md`;
- добавлять аудит как обязательный этап разработки;
- менять Release Approval;
- менять Project State schema;
- заменять PRD или Architecture Document;
- превращать Improvement в обязательный дефект;
- требовать переписать проект ради красоты;
- критиковать без объяснения последствий.

Existing Project Review может рекомендовать глубокий security audit, performance audit, UX research или архитектурное перепроектирование, но такие работы должны запускаться отдельным решением Studio Director.

---

# Definition of Done

Existing Project Review считается завершённым, если:

- Audit Intake Brief создан или принято эквивалентное процессное решение Studio Director;
- review scope зафиксирован;
- requested depth зафиксирован;
- входные источники перечислены;
- missing inputs перечислены;
- ограничения проверки описаны;
- static-only ограничения описаны, если запуск был невозможен;
- Product Review подготовлен Product Analyst или явно отмечен как Not Applicable;
- Architecture Review подготовлен Solution Architect или явно отмечен как Not Applicable;
- Quality Review подготовлен Validator с использованием `CODE_REVIEW_FRAMEWORK.md`;
- findings классифицированы;
- risks описаны;
- improvement opportunities отделены от defects;
- recommended roadmap подготовлен;
- Existing Project Review Report готов для принятия решения Studio Director или заказчиком.
