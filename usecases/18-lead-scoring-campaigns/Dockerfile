# =============================================================================
# Use Case 18 - Lead Scoring & Drip Email Campaigns
# -----------------------------------------------------------------------------
# Scores inbound leads from multiple sources, segments them (hot/warm/cold),
# enrolls them in a drip email sequence and stores results in Baserow.
#
# Build:
#   docker build -t n8n-lead-scoring .
# Run:
#   docker run -d --name n8n-leadscore -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-lead-scoring
# =============================================================================
FROM n8nio/n8n:latest

USER root

# Email/SMTP + IF + Set are built-in. Baserow holds the scoreboard.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-baserow --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_18_LEAD_SCORE_STRONG_KEY \
    LEAD_WEBHOOK_PATH=lead-in

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
