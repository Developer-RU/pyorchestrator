## Страницы

| Раздел | Путь | Описание |
|--------|------|----------|
| Обзор | `/` | KPI, графики runs/load/resources, health |
| Скрипты | `/scripts` | Библиотека объектов, фильтры, bulk actions |
| Редактор | `/scripts/:id` | Monaco, multi-file, run/stop, live logs |
| Группы | `/groups` | Организация скриптов |
| Расписания | `/schedules` | Cron / interval / webhook |
| Вебхуки | `/webhooks` | Inbound HTTP triggers |
| Оповещения | `/notifications` | Alerts по runs |
| Бэкапы | `/backups` | Backup/restore |
| Информация о системе | `/system` | Health, RAM/disk, services |
| MCP сервер | `/mcp` | Документация MCP + статус |
| Пользователи и группы | `/users` | RBAC (Administrator) |
| Настройки | `/settings` | Профиль, тема, язык |

## Роли

| Роль | Возможности |
|------|-------------|
| **Administrator** | Полный доступ, пользователи |
| **Developer** | Скрипты, редактор, schedules |
| **Operator** | Запуск/остановка, просмотр |
| **Viewer** | Только чтение |

## Локализация

Интерфейс: **русский** и **английский** (`Настройки` → язык).

## Live-обновление

Dashboard и списки поддерживают polling (live/static mode). WebSocket — для логов активного run в редакторе.

## Тема

Light / dark / system — переключатель в sidebar header.
