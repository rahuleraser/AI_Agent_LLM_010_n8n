# =============================================================================
# Use Case 06 - CRM Lead Capture & Smart Distribution
# -----------------------------------------------------------------------------
# Captures leads from a landing-page webhook, deduplicates them, scores them
# and distributes to the right HubSpot owner or a local SQLite queue.
#
# Build:
#   docker build -t n8n-crm-leads .
# Run:
#   docker run -d --name n8n-crm -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-crm-leads
# =============================================================================
FROM n8nio/n8n:latest

USER root

# HubSpot is built-in. SQLite adds an offline lead queue / audit log.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-sqlite --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_06_CRM_STRONG_KEY \
    LEAD_WEBHOOK_PATH=lead-capture

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
