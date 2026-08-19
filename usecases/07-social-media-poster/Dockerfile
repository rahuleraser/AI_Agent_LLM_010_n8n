# =============================================================================
# Use Case 07 - Social Media Content Scheduler
# -----------------------------------------------------------------------------
# Generates a weekly content calendar, auto-posts to X (Twitter), Facebook and
# LinkedIn, and mirrors posts to Discord. Social networks are built-in nodes.
#
# Build:
#   docker build -t n8n-social-scheduler .
# Run:
#   docker run -d --name n8n-social -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-social-scheduler
# =============================================================================
FROM n8nio/n8n:latest

USER root

# Twitter/X, LinkedIn and Facebook are built-in. Discord mirrors the posts.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-discord --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_07_SOCIAL_STRONG_KEY \
    GENERIC_TIMEZONE=UTC

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
