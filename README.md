# Incident Management Application

Flask and React application for incident tracking plus CI/CD operation logs.

## Contents

- `app.py`, `routes/`, `backend/api/` - Flask views and JSON APIs.
- `models/` - users, incidents, and pipeline event log models.
- `services/` - DORA metrics, event normalization, alerts, and prediction helpers.
- `templates/` - server-rendered incident and DORA pages.
- `frontend/` - React dashboard.
- `database/schema.sql` - relational schema.
- `tests/` - backend tests.
- `DORA_README.md` - deeper notes for the DORA dashboard and event-time metrics.

## Run With Docker

```bash
docker compose up -d --build
```

The backend is available at http://localhost:5000 and the React frontend at http://localhost:3000.

## CI/CD Operation Log APIs

- `POST /api/observability/events` stores normalized CI/CD events.
- `POST /dora/api/events` stores one pipeline event for authenticated users.
- `POST /dora/api/events/bulk` stores multiple pipeline events.
- `GET /api/observability/metrics/live` returns DORA metrics from logged events.

Example:

```json
{
  "event_id": "evt-001",
  "pipeline_id": "pipeline_001",
  "repository_id": "repo_001",
  "event_type": "DEPLOYMENT_COMPLETED",
  "event_timestamp": "2026-01-01T12:00:00Z",
  "processing_timestamp": "2026-01-01T12:00:02Z",
  "status": "SUCCESS"
}
```

## Tests

```bash
python -m pytest
```
