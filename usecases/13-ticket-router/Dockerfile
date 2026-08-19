# =============================================================================
# Use Case 13 - Customer Support Ticket Router (Zendesk)
# -----------------------------------------------------------------------------
# Listens for new Zendesk tickets, classifies them by department, assigns the
# right agent/team, sets priority and posts a summary to Discord.
#
# Build:
#   docker build -t n8n-ticket-router .
# Run:
#   docker run -d --name n8n-tickets -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-ticket-router
# =============================================================================
FROM n8nio/n8n:latest

USER root

# Zendesk is built-in. Discord gets an instant ticket feed for the team.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-discord --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_13_TICKETS_STRONG_KEY \
    TICKET_WEBHOOK_PATH=ticket-in

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
