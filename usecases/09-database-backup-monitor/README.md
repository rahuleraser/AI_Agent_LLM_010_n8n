# 09 - Database Backup & Uptime Monitor

Schedules automated database backups, stores them in S3/local volumes and alerts the team when a service is down.

## Architecture Diagram

```mermaid
flowchart TD
    A["Cron (Daily 2am)"]
    B["Connect to Database"]
    C["Create Dump / Export"]
    D["Upload to S3 / Volume"]
    E["Health Check Every 5 min"]
    F["IF: Down?"]
    G["Send Alert"]
    H["Log Backup Status"]
    A --> B --> C --> D --> H
    E --> F
    F -- "Yes" --> G
    F -- "No" --> H
```

## Key Nodes

| Node | Purpose |
|------|---------|
| Cron Trigger | Backup schedule |
| MySQL / Postgres | Dump databases |
| MongoDB (community) | Backup MongoDB collections |
| S3 / Local Volume | Store dumps |
| HTTP Request | Health checks |
| IF | Detect downtime |
| Slack / Email | Notify on failure |

## Build & Run

```bash
docker build -t n8n-db-monitor .
docker run -d --name n8n-dbmon -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n n8n-db-monitor
```

Cost: $0 — local backups, S3-compatible free tiers available.
