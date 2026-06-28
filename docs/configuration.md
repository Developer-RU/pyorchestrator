---
layout: default
title: Конфигурация
description: Переменные окружения и настройка сервисов
---

Все переменные — в `.env` (см. `.env.example`).

## Application

| Variable | Default | Description |
|----------|---------|-------------|
| `APP_ENV` | `development` | Окружение |
| `APP_VERSION` | `0.1.0` | Версия в API |

## Security

| Variable | Description |
|----------|-------------|
| `SECRET_MASTER_KEY` | AES key для script secrets (32+ chars) |
| `JWT_SECRET` | Подпись JWT |
| `INTERNAL_API_KEY` | Auth runtime → backend internal API |
| `CORS_ORIGINS` | Разрешённые origins UI |

## Database

| Variable | Default |
|----------|---------|
| `POSTGRES_DB` | `pyorchestrator` |
| `POSTGRES_USER` | `pyorch` |
| `POSTGRES_PASSWORD` | `pyorch_secret` |
| `POSTGRES_PORT` | `5432` |

## Runtime

| Variable | Default | Description |
|----------|---------|-------------|
| `MAX_CONCURRENT_SANDBOXES` | `50` | Параллельные sandbox |
| `DEFAULT_MAX_MEMORY_MB` | `512` | Лимит RAM sandbox |
| `DEFAULT_MAX_CPU_SECONDS` | `300` | CPU time limit |
| `DEFAULT_WALL_TIMEOUT_SEC` | `3600` | Wall timeout |
| `RUNTIME_REPLICAS` | `1` | Prod replicas |

## Frontend

| Variable | Description |
|----------|-------------|
| `VITE_API_URL` | Backend URL для браузера |
| `VITE_WS_URL` | WebSocket URL |
| `FRONTEND_TARGET` | `development` \| `production` |

## MCP

| Variable | Default |
|----------|---------|
| `MCP_PORT` | `8010` |
| `MCP_PYORCH_EMAIL` | admin email |
| `MCP_PYORCH_PASSWORD` | admin password |

## Per-script limits

В UI при создании/редактировании скрипта:

- `max_concurrent_runs`
- `max_runtime_seconds`
- `max_memory_bytes`
- `storage_quota_bytes`

## Grafana

| Variable | Default |
|----------|---------|
| `GRAFANA_ADMIN_USER` | `admin` |
| `GRAFANA_ADMIN_PASSWORD` | `admin` |

Provisioning: `infrastructure/grafana/provisioning/`
