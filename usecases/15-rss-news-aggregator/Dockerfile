# =============================================================================
# Use Case 15 - RSS News Aggregator & Daily Digest
# -----------------------------------------------------------------------------
# Polls multiple RSS feeds, deduplicates and ranks articles by keyword, then
# emails a personal digest and posts top stories to Discord/Telegram.
#
# Build:
#   docker build -t n8n-rss-digest .
# Run:
#   docker run -d --name n8n-rss -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-rss-digest
# =============================================================================
FROM n8nio/n8n:latest

USER root

# RSS Read is built-in. Discord + Telegram deliver the curated digest.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-discord n8n-nodes-telegram --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_15_RSS_STRONG_KEY \
    RSS_WEBHOOK_PATH=rss-digest

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
