# RELEASE_APPROVAL_ALIGNMENT_REPORT.md
v0.1
2026-06-19

## Назначение

Отчёт фиксирует согласование этапа RELEASE APPROVAL с каноническими документами AI Software Studio.

Цель проверки — устранить неопределённости вокруг приёмки заказчиком и зафиксировать единую модель этапа.

---

# Проверенные документы

- `LIFECYCLE.md`
- `agents/STUDIO_DIRECTOR.md`
- `agents/RELEASE_MANAGER.md`
- `DECISION_AUTHORITY.md`

Дополнительно создан новый канонический документ:

- `RELEASE_APPROVAL.md`

---

# Найденные противоречия и неопределённости

## LIFECYCLE.md

Было зафиксировано, что RELEASE APPROVAL существует как этап, но его выход был сведён к упрощённой модели решения заказчика.

Не были явно определены:

- обязательные входные данные этапа;
- материал, который показывается заказчику;
- различие между Validation, Release Approval и Release;
- статус условного одобрения;
- статус полного отказа без доработки;
- последствия каждого решения заказчика.

## agents/STUDIO_DIRECTOR.md

Studio Director был указан как владелец оркестрации, но этап RELEASE APPROVAL не имел достаточной процессной детализации.

Не были явно определены:

- обязанность Studio Director проверить готовность release candidate к согласованию;
- обязательность решения заказчика;
- полный набор возможных решений;
- правила перехода в RELEASE или возврата на предыдущий этап.

## agents/RELEASE_MANAGER.md

Release Manager был владельцем Release Package, но роль в подготовке материалов для RELEASE APPROVAL была недостаточно отделена от этапа RELEASE.

Не были явно определены:

- подготовка Release Candidate Summary;
- запрет формировать Release Package при `Rework Required` или `Rejected`;
- правила обработки `Approved With Conditions`;
- граница между подготовкой approval-материалов и принятием решения заказчиком.

## DECISION_AUTHORITY.md

Документ определял бизнес-решения заказчика, но не выделял RELEASE APPROVAL как плановое бизнес-решение.

Из-за этого оставалась неопределённость: является ли RELEASE APPROVAL технической проверкой, эскалацией или обязательной бизнес-приёмкой.

---

# Принятые решения

## 1. RELEASE APPROVAL является отдельным этапом

Зафиксировано разделение:

- Validation подтверждает качество.
- Release Approval подтверждает соответствие бизнес-требованиям.
- Release фиксирует утверждённый результат.

Эти этапы не заменяют друг друга.

## 2. Владелец этапа — Studio Director

Studio Director:

- запускает RELEASE APPROVAL;
- проверяет готовность материалов;
- передаёт материалы заказчику;
- получает решение заказчика;
- фиксирует решение в Project State;
- выбирает следующий маршрут жизненного цикла.

## 3. Release Manager готовит материалы

Release Manager готовит Release Candidate Summary и обеспечивает понятность approval-материалов для заказчика.

Release Manager не принимает решение за заказчика и не выполняет техническую проверку вместо Validator.

## 4. Заказчик принимает решение

Допустимые статусы решения заказчика:

- `Approved`;
- `Approved With Conditions`;
- `Rework Required`;
- `Rejected`.

## 5. Release Candidate Summary обязателен, но не является каноническим артефактом

Release Candidate Summary признан обязательным материалом согласования.

Он не признан отдельным каноническим артефактом проекта, потому что собирается из существующих источников истины и не должен дублировать PRD, Validation Report, Implementation Reports, Backlog или Release Package.

## 6. Approved With Conditions допустим только для release-level условий

Условное одобрение допустимо, если условие не требует:

- изменения продукта;
- изменения архитектуры;
- новой реализации;
- изменения критериев приёмки;
- повторной Validation.

Если условие требует таких изменений, решение обрабатывается как `Rework Required`.

## 7. Маршрут возврата определяет Studio Director

При `Rework Required` Studio Director выбирает этап возврата по источнику проблемы:

- `PRODUCT DEFINITION`;
- `SOLUTION DESIGN`;
- `PLANNING`;
- `IMPLEMENTATION`;
- `VALIDATION`;
- `RELEASE APPROVAL`, если требуется исправить только материалы согласования.

## 8. Rejected не создаёт Release Package

При `Rejected` проект не переводится в RELEASE.

Решение фиксируется в Project State. Если проект закрывается, Historian получает основание для обновления Project Memory.

---

# Внесённые изменения

## RELEASE_APPROVAL.md

Создан новый канонический документ, который определяет:

- назначение RELEASE APPROVAL;
- владельца этапа;
- входные данные;
- Release Candidate Summary;
- состав информации для заказчика;
- возможные решения заказчика;
- последствия каждого решения;
- обязанности Studio Director;
- обязанности Release Manager;
- правила эскалации;
- связь с Project State;
- примеры `Approved`, `Rework Required` и `Approved With Conditions`.

## LIFECYCLE.md

Обновлён этап RELEASE APPROVAL:

- добавлено разделение Validation, Release Approval и Release;
- добавлены входные данные;
- добавлен Release Candidate Summary;
- расширена модель статусов;
- уточнены критерии завершения;
- уточнено условие входа в RELEASE.

## agents/STUDIO_DIRECTOR.md

Обновлена таблица жизненного цикла:

- вход RELEASE APPROVAL включает Validation Report, PRD, Release Candidate Summary и Project State;
- выход RELEASE APPROVAL включает четыре статуса решения заказчика;
- RELEASE начинается после `Approved` или допустимого `Approved With Conditions`.

Также добавлена ссылка на `documents/RELEASE_APPROVAL.md` и уточнены примеры возврата.

## agents/RELEASE_MANAGER.md

Уточнено, что Release Manager:

- готовит Release Candidate Summary для RELEASE APPROVAL;
- поддерживает Studio Director на этапе согласования;
- формирует Release Package только после допустимого решения RELEASE APPROVAL;
- не формирует утверждённый Release Package при `Rework Required` или `Rejected`;
- отражает условия `Approved With Conditions` в Release Package, если они не требуют возврата.

## DECISION_AUTHORITY.md

Добавлено правило, что RELEASE APPROVAL является плановым бизнес-решением заказчика.

Уточнено, что Validation не заменяет бизнес-приёмку, а Release Approval не используется для технических решений.

---

# Итоговая модель RELEASE APPROVAL

1. Validation завершает независимую проверку качества.
2. Release Manager готовит Release Candidate Summary.
3. Studio Director проверяет готовность материалов.
4. Заказчик получает понятное описание release candidate.
5. Заказчик принимает одно из четырёх решений.
6. Studio Director фиксирует решение в Project State.
7. Проект переходит в RELEASE, возвращается на нужный этап или фиксируется как rejected.

---

# Нерешённые противоречия

Нерешённых противоречий не осталось.

Оставшееся намеренное разграничение:

- Release Candidate Summary является обязательным approval-материалом;
- Release Candidate Summary не является отдельным каноническим артефактом проекта.
