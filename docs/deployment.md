---
layout: default
title: Развёртывание
description: Development и production через Docker Compose
---

## Development (default)

```bash
cp .env.example .env
docker compose up --build
```

- Frontend: Vite dev server с hot reload (`FRONTEND_TARGET=development`)
- Backend: volume mount `./backend/app`
- Все порты опубликованы на localhost

## Production

```bash
cp .env.example .env
# отредактируйте секреты и пароли
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d --build
```

`docker-compose.prod.yml`:

- Frontend — nginx static build
- Runtime — `RUNTIME_REPLICAS` (default 2)
- Postgres/Redis — только internal network
- Prometheus/Grafana — bind `127.0.0.1`

## Чеклист production

- [ ] Сменить `SECRET_MASTER_KEY`, `JWT_SECRET`, `INTERNAL_API_KEY`
- [ ] Сменить `POSTGRES_PASSWORD`, `MINIO_*`, `GRAFANA_ADMIN_PASSWORD`
- [ ] Сменить пароль admin-пользователя
- [ ] Настроить `CORS_ORIGINS` на реальный домен UI
- [ ] TLS termination (nginx/traefik перед frontend + API)
- [ ] Backup schedule в UI
- [ ] Ограничить доступ к портам observability

## Обновление

```bash
git pull
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d --build
```

OTA через UI (`UpdateProvider`) — stub для GitHub releases в v0.1.

## Ресурсы

| Profile | CPU | RAM | Disk |
|---------|-----|-----|------|
| Minimal | 2 | 4 GB | 20 GB |
| Recommended | 4 | 8 GB | 50 GB |
| Heavy (50+ concurrent sandboxes) | 8+ | 16 GB | 100 GB |

## Публикация в GitHub Organization

1. Создайте org `pyorchestrator` (или своё имя)
2. Обновите `docs/_config.yml`: `url`, `baseurl`, `github_org`, `github_repo`
3. Settings → Pages → Source: **GitHub Actions**
4. Push в `main` — workflow `pages.yml` опубликует документацию
