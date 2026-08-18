# Django Application with Docker

Self-contained Django application with Docker and Docker Compose setup.

## Requirements

- Docker Engine + Docker Compose v2
- Python 3.11+ (for local development without Docker)
- `uv` (optional, faster than pip): `pip install uv` or `curl -LsSf https://astral.sh/uv/install.sh | sh`

## Quick Start

### Run with Docker Compose

```bash
docker compose up
```

App runs on `http://localhost:8000`

### Run Locally (without Docker)

Using `uv`:

```bash
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt

python manage.py runserver
```

Or with pip:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

python manage.py runserver
```

## Docker Setup

### Dockerfile

- Base: `python:3.11-slim`
- Installs dependencies from `requirements.txt`
- Runs Django development server on `0.0.0.0:8000`

### docker-compose.yml

- Service: `app` (Django server)
- Port: `8000:8000` (accessible at `localhost:8000`)
- Environment: `PYTHONUNBUFFERED=1` (real-time logs)
- Volume mount: `.:/app` (live code reloading)

## Build

```bash
docker compose build
```

## Logs

```bash
docker compose logs -f app
```

## Stop

```bash
docker compose down
```

## Database

SQLite database (`db.sqlite3`) is persisted on host. Delete to reset.

## Settings

Edit `config/settings.py` for production deployments (ALLOWED_HOSTS, DEBUG, etc).
