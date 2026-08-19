# AI_Agent_LLM_010_n8n

**n8n on Docker Desktop — Lifetime-Free Self-Hosted Workflow Automation + Top 20 Market Use Cases**

This repository provides:

1. A **step-by-step, lifetime-free** n8n installation procedure for **Docker Desktop** that runs 100% on local resources.
2. **20 popular n8n use cases** — each with its **own Dockerfile**, architecture **diagram** and build/run instructions.
3. Everything ready to upload to GitHub and run on your own machine.

---

## Why "Lifetime Free"?

- n8n is **open source** (Sustainable Use License). Self-hosting and running your own workflows is free — unlimited workflows, unlimited executions, unlimited team members.
- Runs entirely on **your** machine inside Docker Desktop — no server rental.
- Data stays in local Docker volumes — no hidden cloud charges.
- No user/workflow/execution limits in the community edition.

---

## Quick Start (Docker Desktop)

```bash
# 1. Pull the official image
docker pull n8nio/n8n:latest

# 2. Run with a persistent local volume
docker run -d --name n8n -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  -e N8N_ENCRYPTION_KEY="$(openssl rand -hex 32)" \
  n8nio/n8n:latest

# 3. Open http://localhost:5678 and create your free local account
```

Full guide: [docs/n8n-docker-desktop-installation.md](docs/n8n-docker-desktop-installation.md)

### Production-style local stack (n8n + PostgreSQL)

```bash
cp docker/.env.example docker/.env   # then edit docker/.env
docker compose -f docker/docker-compose.yml --env-file docker/.env up -d
```

---

## Repository Structure

```
├── docs/
│   └── n8n-docker-desktop-installation.md   # Step-by-step lifetime-free install guide
├── docker/
│   ├── base/Dockerfile.n8n                  # Base n8n image
│   ├── docker-compose.yml                   # n8n + PostgreSQL local stack
│   └── .env.example                         # Environment template
├── scripts/
│   └── build-all.sh                         # Build base + all 20 use-case images
└── usecases/
    ├── 01-gmail-inbox-processor/            # Dockerfile + diagram + README
    ├── 02-slack-team-alerts/
    ├── ... (20 total)
    └── 20-api-aggregation-gateway/
```

---

## Top 20 n8n Use Cases (Famous in the Market)

| # | Use Case | Folder | Community Nodes | Diagram |
|---|----------|--------|-----------------|---------|
| 01 | Gmail Inbox Processor & Auto-Responder | `usecases/01-gmail-inbox-processor` | - | [diagram](usecases/01-gmail-inbox-processor/README.md) |
| 02 | Slack Team Alert & Notification System | `usecases/02-slack-team-alerts` | Discord | [diagram](usecases/02-slack-team-alerts/README.md) |
| 03 | Telegram Message & Notification Bot | `usecases/03-telegram-message-bot` | Telegram | [diagram](usecases/03-telegram-message-bot/README.md) |
| 04 | Web Scraper & Data Extraction | `usecases/04-web-scraper-data-extractor` | - | [diagram](usecases/04-web-scraper-data-extractor/README.md) |
| 05 | E-commerce Order Sync (Shopify to Sheets) | `usecases/05-shopify-order-sync` | Stripe | [diagram](usecases/05-shopify-order-sync/README.md) |
| 06 | CRM Lead Capture & Smart Distribution | `usecases/06-crm-lead-capture` | SQLite | [diagram](usecases/06-crm-lead-capture/README.md) |
| 07 | Social Media Content Scheduler | `usecases/07-social-media-poster` | Discord | [diagram](usecases/07-social-media-poster/README.md) |
| 08 | PDF Invoice Generator & Delivery | `usecases/08-invoice-generator` | MongoDB | [diagram](usecases/08-invoice-generator/README.md) |
| 09 | Database Backup & Uptime Monitor | `usecases/09-database-backup-monitor` | MongoDB, SQLite | [diagram](usecases/09-database-backup-monitor/README.md) |
| 10 | AI / LLM Powered Chat Assistant | `usecases/10-ai-llm-chatbot` | MCP, OpenWeatherMap | [diagram](usecases/10-ai-llm-chatbot/README.md) |
| 11 | Web Form Data Pipeline | `usecases/11-form-data-pipeline` | Baserow | [diagram](usecases/11-form-data-pipeline/README.md) |
| 12 | Sales Analytics & BI Pipeline | `usecases/12-sales-dashboard-pipeline` | Baserow | [diagram](usecases/12-sales-dashboard-pipeline/README.md) |
| 13 | Customer Support Ticket Router (Zendesk) | `usecases/13-ticket-router` | Discord | [diagram](usecases/13-ticket-router/README.md) |
| 14 | Invoice & Payment Reminder Automation | `usecases/14-payment-reminders` | Stripe, SQLite | [diagram](usecases/14-payment-reminders/README.md) |
| 15 | RSS News Aggregator & Daily Digest | `usecases/15-rss-news-aggregator` | Discord, Telegram | [diagram](usecases/15-rss-news-aggregator/README.md) |
| 16 | GitHub Issue & PR Automation | `usecases/16-github-dev-workflows` | GitHub | [diagram](usecases/16-github-dev-workflows/README.md) |
| 17 | Cloud Storage Sync & Backup (Drive/S3) | `usecases/17-cloud-file-sync` | MongoDB | [diagram](usecases/17-cloud-file-sync/README.md) |
| 18 | Lead Scoring & Drip Email Campaigns | `usecases/18-lead-scoring-campaigns` | Baserow | [diagram](usecases/18-lead-scoring-campaigns/README.md) |
| 19 | Weather Alerts & Smart Notifications | `usecases/19-weather-alert-system` | OpenWeatherMap, Telegram | [diagram](usecases/19-weather-alert-system/README.md) |
| 20 | Multi-API Aggregation & Enrichment Gateway | `usecases/20-api-aggregation-gateway` | MCP, Stripe, Zoom | [diagram](usecases/20-api-aggregation-gateway/README.md) |

---

## Build All Images at Once

```bash
./scripts/build-all.sh
```

Each use case also builds individually:

```bash
cd usecases/10-ai-llm-chatbot
docker build -t n8n-ai-chatbot .
docker run -d --name n8n-ai -p 5678:5678 -v ~/.n8n:/home/node/.n8n n8n-ai-chatbot
```

---

## Notes & Best Practices

- Set a unique `N8N_ENCRYPTION_KEY` before creating workflows, otherwise encrypted credentials can be lost on container recreation.
- Enable `N8N_BASIC_AUTH_ACTIVE=true` and set a strong password for local login.
- All community node packages referenced in the Dockerfiles were verified against the npm registry.
- Keep your workflows exported as JSON files in version control for backup.

## License

This repository is a reference guide and set of Dockerfiles for n8n.
n8n itself is licensed under the Sustainable Use License — free for self-hosting and commercial use of your own workflows.
