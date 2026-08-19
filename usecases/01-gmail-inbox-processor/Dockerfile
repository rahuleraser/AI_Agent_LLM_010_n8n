# =============================================================================
# Use Case 01 - Gmail Inbox Processor & Auto-Responder
# -----------------------------------------------------------------------------
# Watches your Gmail inbox, classifies incoming mail, auto-responds to common
# queries and files important emails into Google Sheets for follow-up.
# Uses n8n built-in Gmail, Sheets, Cron and IF nodes. No paid API required.
#
# Build:
#   docker build -t n8n-gmail-inbox .
# Run:
#   docker run -d --name n8n-gmail -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-gmail-inbox
# =============================================================================
FROM n8nio/n8n:latest

USER root

# This use case relies on built-in nodes (Gmail, Google Sheets, Cron, IF, Filter).
# Install a community node when you want AI-assisted email drafting later:
# RUN cd /usr/local/lib/node_modules/n8n \
#     && npm install n8n-nodes-mcp --save \
#     && npm cache clean --force

# Mail-polling workflow friendly settings
ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_01_GMAIL_STRONG_KEY \
    GENERIC_TIMEZONE=UTC

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
