## Принцип

Пользовательские скрипты **не получают отдельный Docker-контейнер**. Все runs выполняются как **изолированные subprocess** внутри сервиса `runtime`.

```
Runtime Engine
├── Redis BLPOP runtime:jobs
├── SandboxPool (semaphore max_concurrent)
│   └── Sandbox per run
│       ├── venv (per workspace)
│       ├── subprocess python entrypoint
│       ├── RLIMIT_CPU / RLIMIT_AS
│       └── wall-clock timeout
└── POST /internal/runs/* → backend
```

## Жизненный цикл run

1. **Queue** — backend создаёт `Run` (status `queued`), кладёт job в Redis
2. **Start** — runtime забирает job, вызывает `/internal/runs/start`
3. **Execute** — sandbox запускает `entrypoint` с secrets в env (`SECRET_*`)
4. **Logs** — stdout/stderr → WebSocket + PostgreSQL
5. **Complete** — exit code, duration → `/internal/runs/complete`
6. **Stop** — UI публикует `stop` в `run:{id}:control`, SIGTERM процессу

## Изоляция

| Слой | Механизм |
|------|----------|
| Process | `subprocess.Popen` |
| FS | `/workspaces/{script_id}/{run_id}/` |
| Deps | `pip install -r requirements.txt` в local venv |
| CPU/Memory | `resource.setrlimit` |
| Time | `asyncio.wait_for` wall timeout |
| Secrets | Encrypted at rest, injected at run time |

## Масштабирование

`docker compose -f docker-compose.prod.yml` — несколько реплик `runtime`, общая Redis-очередь.

## Hot reload кода

Сохранение скрипта в UI → Redis `script:updated` → runtime инвалидирует venv cache → следующий run с новым кодом **без перезапуска контейнеров**.
