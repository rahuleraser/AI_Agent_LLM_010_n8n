# 17 - Cloud Storage Sync & Backup (Drive / S3)

Watches Google Drive and S3 buckets, syncs changes both ways, deduplicates, logs to MongoDB and emails a sync report.

## Architecture Diagram

```mermaid
flowchart TD
    A["Google Drive Trigger"]
    B["S3 Polling / Webhook"]
    C["Compare State (DB)"]
    D["Sync Drive to S3"]
    E["Sync S3 to Drive"]
    F["Rename Duplicates"]
    G["Log to MongoDB"]
    H["Email Sync Report"]
    A --> C
    B --> C
    C -- "New/Changed" --> D --> F
    C -- "New/Changed" --> E --> F
    D --> G --> H
    E --> G --> H
```

## Key Nodes

| Node | Purpose |
|------|---------|
| Google Drive | Watch + read files |
| S3 | Bucket operations |
| MongoDB (community) | Sync state / audit log |
| Code / IF | Conflict resolution |
| Rename | Avoid duplicates |
| Email | Daily sync report |

## Build & Run

```bash
docker build -t n8n-cloud-sync .
docker run -d --name n8n-cloudsync -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n n8n-cloud-sync
```

Cost: $0 — Google Drive free 15GB, MinIO/S3-compatible local storage.
