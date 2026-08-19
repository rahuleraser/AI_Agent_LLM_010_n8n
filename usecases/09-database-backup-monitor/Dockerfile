# =============================================================================
# Use Case 09 - Database Backup & Uptime Monitor
# -----------------------------------------------------------------------------
# Monitors your databases (MySQL/Postgres/Mongo), schedules automated backups,
# uploads dumps to cloud storage and alerts the team when a service is down.
#
# Build:
#   docker build -t n8n-db-monitor .
# Run:
#   docker run -d --name n8n-dbmon -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-db-monitor
# =============================================================================
FROM n8nio/n8n:latest

USER root

# Postgres/MySQL/S3 are built-in. MongoDB + SQLite add local backup targets.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-mongodb n8n-nodes-sqlite --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_09_DB_MONITOR_STRONG_KEY \
    BACKUP_CRON=0 2 * * * \
    MONITOR_INTERVAL_MINUTES=5

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
