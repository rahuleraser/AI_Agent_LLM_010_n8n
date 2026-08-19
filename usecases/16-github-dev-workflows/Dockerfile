# =============================================================================
# Use Case 16 - GitHub Issue & PR Automation
# -----------------------------------------------------------------------------
# Watches GitHub issues/PRs, auto-labels them, assigns reviewers, comments a
# welcome message, sends PR notifications and posts to Slack/Discord.
#
# Build:
#   docker build -t n8n-github-workflows .
# Run:
#   docker run -d --name n8n-github -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-github-workflows
# =============================================================================
FROM n8nio/n8n:latest

USER root

# GitHub community node (issues, PRs, repos, actions, labels) on top of the
# built-in HTTP trigger for webhooks.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-github --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_16_GITHUB_STRONG_KEY \
    GITHUB_WEBHOOK_PATH=github-events

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
