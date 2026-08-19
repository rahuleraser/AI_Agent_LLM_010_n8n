# =============================================================================
# Use Case 03 - Telegram Message & Notification Bot
# -----------------------------------------------------------------------------
# Sends order updates, alerts and daily digests to Telegram. Community
# n8n-nodes-telegram node gives full bot + channel support.
#
# Build:
#   docker build -t n8n-telegram-bot .
# Run:
#   docker run -d --name n8n-telegram -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-telegram-bot
# =============================================================================
FROM n8nio/n8n:latest

USER root

# Official community Telegram nodes (bot triggers + send message actions).
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-telegram --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_03_TELEGRAM_STRONG_KEY \
    TELEGRAM_BOT_TOKEN=PASTE_YOUR_BOT_TOKEN_HERE \
    TELEGRAM_CHAT_ID=PASTE_YOUR_CHAT_ID_HERE

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
