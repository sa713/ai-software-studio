# V02_AUDIT_READINESS_REVIEW.md
v0.2
2026-06-22

## Current State

AI Software Studio v0.2 уже получила базовые элементы для экспертной работы:

- Product Analyst v0.2 усилен до Business Analysis внутри Discovery;
- Validator v0.2 выполняет Compliance Review и Expert Review;
- `CODE_REVIEW_FRAMEWORK.md` задаёт единый стандарт технической оценки;
- `EXISTING_PROJECT_REVIEW.md` описывает отдельный режим Existing Project Review;
- `ARTIFACTS.md` содержит структуру Existing Project Review Report.

Текущий основной lifecycle разработки не изменён.

Existing Project Review описан как отдельный режим:

```text
Existing Project
↓
Audit
↓
Review
↓
Improvement Proposal
```

В режиме используются существующие роли:

- Product Analyst;
- Solution Architect;
- Validator;
- Studio Director для оркестрации.

Новая роль Auditor не создана.

---

## Strengths

1. Базовая модель аудита уже понятна.

Есть отдельный документ `EXISTING_PROJECT_REVIEW.md`, который объясняет цель режима, входы, маршрут, роли и итоговый артефакт.

2. Основной lifecycle защищён.

Existing Project Review явно не заменяет `LIFECYCLE.md`, не добавляет этапы разработки и не меняет Project State schema.

3. Есть единая модель технической оценки.

`CODE_REVIEW_FRAMEWORK.md` покрывает:

- Architecture Review;
- Code Quality Review;
- Security Review;
- Maintainability Review;
- Dependency Review;
- Test Coverage Review.

4. Есть единая модель findings.

Defect, Risk, Improvement и Subjective Preference уже описаны и могут применяться как в Validation, так и в Existing Project Review.

5. Итоговый отчёт ориентирован на решение.

Existing Project Review Report содержит Executive Summary, риски, улучшения и Recommended Roadmap, поэтому результат потенциально понятен заказчику.

6. Роли используются естественно.

Product Analyst анализирует продуктовую сторону, Solution Architect — архитектуру, Validator — качество реализации через Code Review Framework.

---

## Gaps

### Gap 1. Нет минимального Audit Intake

Сейчас Existing Project Review говорит, что Studio Director фиксирует цель, scope и входные источники, но не задаёт минимальную структуру стартового запроса.

Перед реальным аудитом не хватает Audit Intake Brief с полями:

- reviewed system;
- audit goal;
- target audience;
- business context;
- known concerns;
- repository or source location;
- available documentation;
- access limitations;
- expected depth;
- out of scope;
- deadline or urgency.

Без этого первый аудит будет начинаться с ручной договорённости.

### Gap 2. Не разделены обязательные и необязательные входные данные

`EXISTING_PROJECT_REVIEW.md` перечисляет возможные источники, но не определяет, что минимально достаточно для разных видов аудита.

Например:

- для code-heavy review достаточно репозитория и инструкции запуска;
- для product review нужен хотя бы контекст пользователей и назначения системы;
- для architecture review желательно иметь README, схему или возможность восстановить архитектуру по коду;
- для security review нужны конфигурации и сведения об окружении, иначе проверка ограничена.

Без этого Studio Director должен каждый раз вручную решать, можно ли начинать.

### Gap 3. Не определены уровни глубины аудита

Сейчас режим не различает:

- quick scan;
- focused review;
- full review;
- pre-refactoring review;
- production readiness review.

Для Photo365, AI Editorial Office и Telegram-бота глубина проверки будет разной. Без уровней глубины команда может ожидать "полный аудит", а фактически получить ограниченный review.

### Gap 4. Ролевые инструкции ещё привязаны к development lifecycle

Product Analyst v0.2 описан как владелец Discovery и ожидает Idea Brief.

Validator v0.2 описан как владелец Validation и ожидает Validation Scope, Implementation Report, Task Specification, Backlog, Architecture Document и PRD.

Для существующего проекта этих артефактов часто не будет.

`EXISTING_PROJECT_REVIEW.md` разрешает использовать Product Analyst и Validator, но их персональные инструкции пока не объясняют, как действовать в audit mode без Idea Brief, PRD, Task Specification и Implementation Report.

Это главный практический blocker.

### Gap 5. Возможен overlap между Solution Architect и Validator

Solution Architect отвечает за Architecture Review.

Validator по `CODE_REVIEW_FRAMEWORK.md` тоже выполняет Architecture Review в части качества реализации.

Разделение пока описано только частично.

Нужно явно разделить:

- Solution Architect оценивает архитектурную структуру, решения, границы, системные риски;
- Validator оценивает качество реализации и evidence по framework;
- если оба находят архитектурную проблему, она должна быть объединена в одну finding или связана через source role.

Без этого отчёт может получить два разных Architecture Review с разными рекомендациями.

### Gap 6. Не определён владелец итоговой сборки отчёта

`ARTIFACTS.md` говорит, что report owner — назначенная Studio Director роль, а по умолчанию итоговую сборку выполняет Validator, если есть Quality Review.

Но Existing Project Review Report включает Executive Summary и Recommended Roadmap, которые требуют синтеза Product, Architecture и Quality выводов.

Validator может быть не лучшим владельцем продуктово-архитектурного синтеза.

Нужно уточнить:

- кто собирает Executive Summary;
- кто приоритизирует Recommended Roadmap;
- кто разрешает конфликт между ролями;
- кто делает финальную редакцию customer-facing вывода.

### Gap 7. Нет правил приоритизации roadmap

Recommended Roadmap содержит группы, но не описывает, как назначать Priority.

Не хватает минимальной модели:

- Critical;
- High;
- Medium;
- Low;
- Later.

И критериев:

- user impact;
- operational risk;
- security risk;
- effort;
- dependency;
- confidence.

Без этого roadmap может стать списком правильных, но неупорядоченных улучшений.

### Gap 8. Risks и Improvement Opportunities могут дублировать role sections

Product Review, Architecture Review и Quality Review уже содержат Observation, Consequence, Recommendation.

Risks и Improvement Opportunities повторяют часть тех же выводов.

Это допустимо как consolidated summary, но документ не говорит, должны ли эти разделы:

- дублировать findings полностью;
- ссылаться на source findings;
- содержать только top-level consolidated items.

Без правила отчёт может стать повторяющимся.

### Gap 9. Нет идентификаторов findings

В Existing Project Review Report нет обязательного `Finding ID`.

Без ID сложно:

- связать risk с source observation;
- связать improvement с roadmap item;
- отслеживать исправления после аудита;
- сравнивать несколько аудитов одного проекта.

### Gap 10. Не описаны правила evidence для audit mode

Code Review Framework требует evidence, но Existing Project Review не уточняет уровни evidence для существующего проекта.

Например:

- direct code evidence;
- missing documentation;
- runtime behavior;
- repository structure;
- dependency metadata;
- interview/customer statement.

Для реального аудита важно отличать подтверждённый дефект от гипотезы, особенно если проект нельзя запустить.

### Gap 11. Security Review может быть misunderstood

Framework говорит, что Security Review не является pentest.

Но Existing Project Review Report не требует явно указать security limitations.

Для реального клиента это риск ожиданий: заказчик может прочитать "Security Review" как гарантию безопасности.

### Gap 12. Не описан режим "project cannot be run"

Для существующих проектов часто нет рабочей инструкции запуска, секретов, окружения или тестовой базы.

Сейчас это можно записать как limitation, но нет явного правила:

- что делать, если проект нельзя запустить;
- какие выводы допустимы только по static review;
- как помечать невозможность runtime validation.

### Gap 13. Нет явного правила для confidential/secrets handling

Аудит реального репозитория может включать секреты, токены, персональные данные или production configs.

Документы не описывают:

- как фиксировать найденные секреты без раскрытия значения;
- как не копировать секреты в report;
- как описывать sensitive evidence безопасно.

### Gap 14. Не описан формат customer-facing vs internal detail

Existing Project Review Report должен быть понятен заказчику и не быть простынёй.

Но для команды может понадобиться технический appendix.

Сейчас Appendix допустим, но нет правила:

- Executive Summary и Recommended Roadmap должны быть customer-facing;
- technical evidence может уходить в Appendix;
- секреты и sensitive data не копируются.

### Gap 15. Нет явного completion gate для готовности отчёта

Definition of Done есть, но не хватает финальной проверки:

- все sections согласованы;
- top risks отражены в Executive Summary;
- roadmap связан с findings;
- limitations явно указаны;
- customer can act on the report.

---

## Ambiguities

### Ambiguity 1. Что считается началом аудита

Неясно, достаточно ли фразы "посмотри этот репозиторий" или нужен формальный review scope от Studio Director.

Практически лучше считать аудит начатым только после Audit Intake Brief или эквивалентного решения Studio Director.

### Ambiguity 2. Какой артефакт создаётся первым

Existing Project Review Report является итоговым артефактом, но неясно, нужен ли промежуточный Audit Scope.

Без промежуточного scope роли могут начать проверку с разными ожиданиями.

### Ambiguity 3. Как распределяется работа между ролями во времени

Возможные варианты:

- Product Analyst сначала формирует product context, затем Solution Architect и Validator проверяют код;
- все роли работают параллельно;
- Validator сначала делает static scan, затем Product Analyst проверяет user-facing gaps.

Документ не выбирает порядок.

### Ambiguity 4. Как обрабатывать отсутствие Product Review

Для чисто технического репозитория может не быть продуктового контекста.

Сейчас допускается Not Applicable, но неясно, когда Product Review можно пропустить, а когда это limitation.

### Ambiguity 5. Как отличать Architecture Review от Quality Review

Оба раздела могут говорить о:

- компонентах;
- зависимостях;
- масштабируемости;
- архитектурном долге.

Нужны границы, иначе будет дублирование и риск конфликтующих рекомендаций.

### Ambiguity 6. Какой статус имеет Recommended Roadmap

Документ говорит, что roadmap не является Backlog и не создаёт обязательства реализации.

Но неясно, является ли это предложением Studio Director, рекомендацией ролей или customer-facing планом.

### Ambiguity 7. Как работать с существующими GitHub issues

Issues и backlog указаны как возможные входы, но не описано, как учитывать:

- known bugs;
- stale issues;
- customer-reported problems;
- planned work.

### Ambiguity 8. Как оценивать AI-агентов

Code Review Framework покрывает код, безопасность, зависимости и тесты, но AI-агенты требуют дополнительных аспектов:

- prompt behavior;
- tool permissions;
- memory/state handling;
- hallucination risk;
- evaluation quality;
- human approval boundaries.

Сейчас это можно частично покрыть Security, Test Coverage и Architecture Review, но критерии не названы явно.

---

## Real Scenario Dry Run

### Photo365

Вероятный вход:

- мобильное или веб-приложение;
- пользовательские сценарии вокруг фото;
- репозиторий;
- возможно, дизайн/документация;
- возможно, backend/API.

Что сработает:

- Product Analyst сможет искать отсутствующие роли, сценарии, support/monitoring gaps;
- Solution Architect сможет оценить структуру приложения, backend, storage и integrations;
- Validator сможет применить Code Review Framework.

Где процесс может сломаться:

- непонятно, какой scope: всё приложение, только backend, только mobile, только release readiness;
- без product context Product Review будет строиться на предположениях;
- без инструкции запуска Quality Review станет static-only;
- фото/медиа данные создают privacy/storage risks, но нет специального intake вопроса про данные;
- Recommended Roadmap может смешать product gaps, architecture debt и code fixes без общей модели приоритетов.

### AI Editorial Office

Вероятный вход:

- AI workflow;
- prompts;
- agents/tools;
- content pipeline;
- editorial roles;
- repository and docs.

Что сработает:

- Product Analyst сможет выявить missing editorial roles, approval flow, support process;
- Solution Architect сможет оценить agent/tool boundaries and data flow;
- Validator сможет проверить code quality, tests, dependencies, security basics.

Где процесс может сломаться:

- Code Review Framework не называет AI-specific review criteria;
- unclear handling of prompts, model configs, evaluation sets and human approval;
- security review may miss tool permission and content leakage risks if not explicitly scoped;
- Test Coverage Review may not know whether prompt/evaluation tests count as tests;
- Product Review and Architecture Review can overlap around editorial workflow ownership.

### Existing Telegram Bot

Вероятный вход:

- repository;
- bot token/configs;
- deployment notes;
- logs or known issues;
- database schema.

Что сработает:

- Validator can inspect dependencies, secrets, error handling, tests;
- Solution Architect can inspect bot handlers, storage, scheduling, integrations;
- Product Analyst can inspect admin/operator/support scenarios.

Где процесс может сломаться:

- high chance of secrets in config, but no safe evidence handling rule;
- often no PRD or architecture docs, so Validator role instruction may treat missing artifacts as blocker;
- no explicit runtime limitation handling if bot cannot be run without production token;
- admin/support scenarios may be undocumented and require customer input;
- roadmap prioritization is needed to separate critical token/security fixes from nice-to-have UX changes.

---

## Recommended Fixes

### Fix 1. Add Audit Intake Brief

Create a minimal intake template inside `EXISTING_PROJECT_REVIEW.md` or `ARTIFACTS.md`.

Minimum fields:

- Reviewed System;
- Audit Goal;
- Review Scope;
- Out Of Scope;
- Available Inputs;
- Missing Inputs;
- Access Limitations;
- Target Audience;
- Expected Depth;
- Known Concerns;
- Deadline or Urgency.

### Fix 2. Define required vs optional inputs

Add a small table:

- minimum for any review;
- minimum for Product Review;
- minimum for Architecture Review;
- minimum for Quality Review;
- optional but useful inputs.

### Fix 3. Add audit depth levels

Define:

- Quick Scan;
- Focused Review;
- Full Review;
- Production Readiness Review.

This will prevent unrealistic expectations.

### Fix 4. Add audit-mode instructions to Product Analyst and Validator

Product Analyst should know how to work without Idea Brief when assigned to Existing Project Review.

Validator should know how to work without PRD, Task Specification, Backlog and Implementation Report when assigned to Existing Project Review.

This is the most important fix before a real audit.

### Fix 5. Clarify Solution Architect vs Validator boundary

Add a short responsibility split:

- Solution Architect owns system-level architecture assessment;
- Validator owns implementation quality assessment using Code Review Framework;
- overlapping findings must be merged or cross-referenced.

### Fix 6. Define report assembly owner

Clarify who owns:

- Executive Summary;
- consolidation of risks;
- Recommended Roadmap;
- final report consistency.

Recommended default: Studio Director owns final synthesis or explicitly assigns one existing role as report owner per review.

### Fix 7. Add Finding ID and Source Role

Existing Project Review Report should include:

- Finding ID;
- Source Role;
- Source Section;
- Related Roadmap Item.

This will make report actionable after the audit.

### Fix 8. Add roadmap priority model

Define priority levels and criteria.

Suggested levels:

- Critical;
- High;
- Medium;
- Low;
- Later.

Suggested criteria:

- user impact;
- operational risk;
- security risk;
- implementation effort;
- dependency;
- confidence.

### Fix 9. Add safe handling of secrets and sensitive evidence

Rules:

- never copy secret values into report;
- mask tokens and credentials;
- describe location and risk without exposing sensitive value;
- mark security evidence as sensitive if needed.

### Fix 10. Add static-only review rule

If project cannot be run:

- mark runtime validation as Not Performed;
- classify runtime uncertainty as Risk;
- distinguish static findings from observed behavior;
- explain confidence level.

### Fix 11. Add AI-agent-specific review prompts

Extend Code Review Framework or Existing Project Review guidance with optional AI-agent checks:

- prompt and instruction boundaries;
- tool permissions;
- memory/state behavior;
- human approval points;
- evaluation coverage;
- output safety and content quality risks.

### Fix 12. Add report compactness rule

Keep Executive Summary and Recommended Roadmap customer-facing.

Move detailed evidence to Appendix.

Use consolidated Risks and Improvement Opportunities, not duplicated role-section text.

---

## Auditor Role Assessment

There is not enough evidence to create a separate Auditor role now.

Arguments against creating Auditor now:

- role responsibilities can be covered by Product Analyst, Solution Architect and Validator;
- the biggest blockers are process clarity and input/report structure, not missing ownership;
- creating Auditor before real audits would violate the roadmap warning not to create the role prematurely;
- a new role could duplicate Validator and Solution Architect responsibilities.

Potential argument for Auditor later:

- if real audits repeatedly fail because nobody owns synthesis, prioritization and final customer-facing report quality, a dedicated role may become useful.

Current recommendation:

- do not create Auditor now;
- run at least two or three real audits with existing roles;
- track whether synthesis/report ownership repeatedly causes friction;
- decide later through `STUDIO_IMPROVEMENT_PROCESS.md` if a role is justified.

---

## Readiness Verdict

Студия почти готова к первому реальному аудиту, но не полностью готова к repeatable audit без ручных договорённостей.

Можно провести пилотный аудит уже сейчас, если Studio Director вручную задаст:

- audit intake;
- scope;
- depth;
- available inputs;
- limitations;
- report owner;
- priority model.

Без этих ручных решений процесс может стать неоднозначным, особенно для AI Editorial Office и Telegram-ботов.

Минимальные доработки перед первым реальным аудитом:

1. Audit Intake Brief.
2. Required vs optional inputs.
3. Audit depth levels.
4. Audit-mode instructions for Product Analyst and Validator.
5. Report owner and roadmap priority rules.
6. Secret/sensitive evidence handling.

После этих доработок Студия будет готова проводить реальные аудиты значительно устойчивее.
