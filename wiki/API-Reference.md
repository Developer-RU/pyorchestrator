Base URL: `http://localhost:8000/api/v1`

Интерактивная документация: **http://localhost:8000/docs** (Swagger UI)

## Auth

```http
POST /api/v1/auth/login
Content-Type: application/json

{"email": "admin@pyorchestrator.local", "password": "admin"}
```

Response: `{ "access_token": "...", "token_type": "bearer" }`

Далее: `Authorization: Bearer <token>`

## Scripts

| Method | Path | Description |
|--------|------|-------------|
| GET | `/scripts` | List scripts |
| POST | `/scripts` | Create |
| GET | `/scripts/{id}` | Get |
| PATCH | `/scripts/{id}` | Update |
| DELETE | `/scripts/{id}` | Delete |
| GET | `/scripts/{id}/files` | List files |
| PUT | `/scripts/{id}/files/{path}` | Save file |

## Runs

| Method | Path | Description |
|--------|------|-------------|
| POST | `/runs/scripts/{id}/run` | Queue run |
| POST | `/runs/scripts/{id}/stop` | Stop running/queued |
| GET | `/runs/scripts/{id}/runs` | History |
| GET | `/runs/{run_id}` | Run status |
| GET | `/runs/{run_id}/logs` | Logs |

## Schedules & Webhooks

| Method | Path |
|--------|------|
| GET/POST | `/schedules` |
| PATCH/DELETE | `/schedules/{id}` |
| GET/POST | `/webhooks` |
| POST | `/hooks/{token}` | Public webhook invoke |

## System

| Method | Path |
|--------|------|
| GET | `/system/info` |
| GET | `/mcp/info` |
| GET | `/dashboard/stats` |
| GET | `/dashboard/timeseries` |

## WebSocket

```
ws://localhost:8000/ws/runs/{run_id}
```

Live log stream (JWT in connection or cookie per deployment).

## Metrics

Prometheus: `http://localhost:8000/metrics` (backend), runtime `:9093`
