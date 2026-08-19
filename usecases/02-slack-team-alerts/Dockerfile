# =============================================================================
# Use Case 02 - Slack Team Alert & Notification System
# -----------------------------------------------------------------------------
# Aggregates alerts from multiple sources (forms, monitoring, payments) and
# routes them to the right Slack channel. Includes a Discord mirror channel.
#
# Build:
#   docker build -t n8n-slack-alerts .
# Run:
#   docker run -d --name n8n-slack -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-slack-alerts
# =============================================================================
FROM n8nio/n8n:latest

USER root

# Slack is built-in; add Discord as an extra alerting channel.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-discord --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_02_SLACK_STRONG_KEY

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
