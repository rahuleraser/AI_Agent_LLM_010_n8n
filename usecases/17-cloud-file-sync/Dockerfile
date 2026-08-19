# =============================================================================
# Use Case 17 - Cloud Storage Sync & Backup (Drive / S3)
# -----------------------------------------------------------------------------
# Watches folders in Google Drive and S3-compatible buckets, syncs changes in
# both directions, renames duplicates, logs every action to MongoDB and emails
# a sync report.
#
# Build:
#   docker build -t n8n-cloud-sync .
# Run:
#   docker run -d --name n8n-cloudsync -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-cloud-sync
# =============================================================================
FROM n8nio/n8n:latest

USER root

# Google Drive + S3 are built-in. MongoDB keeps a local sync audit log.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-mongodb --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_17_CLOUD_SYNC_STRONG_KEY \
    SYNC_WEBHOOK_PATH=sync-trigger

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
