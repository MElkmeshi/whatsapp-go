# WuzAPI

WhatsApp HTTP API powered by [wuzapi](https://github.com/asternic/wuzapi), backed by PostgreSQL and RabbitMQ. Runs entirely through Docker Compose.

## Stack

- **wuzapi-server** — WhatsApp API (port `8080`)
- **db** — PostgreSQL 16
- **rabbitmq** — RabbitMQ 3 with management UI (ports `5672`, `15672`)

## Setup

1. Copy the example env file and fill in secrets:

   ```sh
   cp .env.example .env
   ```

   Generate fresh secrets if needed:

   ```sh
   openssl rand -hex 16   # WUZAPI_ADMIN_TOKEN
   openssl rand -hex 32   # WUZAPI_GLOBAL_ENCRYPTION_KEY
   openssl rand -hex 32   # WUZAPI_GLOBAL_HMAC_KEY
   ```

2. Start the stack:

   ```sh
   docker compose up -d
   ```

3. Check it's running:

   ```sh
   docker compose ps
   ```

## Services

| Service     | URL                          |
| ----------- | ---------------------------- |
| WuzAPI      | http://localhost:8080        |
| RabbitMQ UI | http://localhost:15672       |

RabbitMQ default credentials: `wuzapi` / `wuzapi`.

## Environment Variables

See [.env.example](./.env.example) for the full list. Required:

- `WUZAPI_ADMIN_TOKEN` — admin auth token
- `WUZAPI_GLOBAL_ENCRYPTION_KEY` — 32-byte hex key

Optional:

- `WUZAPI_GLOBAL_HMAC_KEY`, `WUZAPI_GLOBAL_WEBHOOK`, `WEBHOOK_FORMAT`
- `DB_USER`, `DB_PASSWORD`, `DB_NAME`, `DB_PORT`
- `TZ`, `SESSION_DEVICE_NAME`

## Common commands

```sh
docker compose logs -f wuzapi-server   # tail API logs
docker compose down                    # stop stack
docker compose down -v                 # stop and wipe volumes
```
