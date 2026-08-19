# =============================================================================
# Use Case 20 - Multi-API Aggregation & Enrichment Gateway
# -----------------------------------------------------------------------------
# Single webhook endpoint that fans out a request to multiple external APIs
# (CRM, payment, meeting, weather), merges and deduplicates the responses,
# enriches via MCP tools and returns one combined JSON payload.
#
# Build:
#   docker build -t n8n-api-gateway .
# Run:
#   docker run -d --name n8n-gateway -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-api-gateway
# =============================================================================
FROM n8nio/n8n:latest

USER root

# MCP gives the aggregation layer live tool access; Stripe + Zoom are
# representative external API modules you can fan out to.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-mcp n8n-nodes-stripe n8n-nodes-zoom --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_20_API_GATEWAY_STRONG_KEY \
    AGGREGATE_WEBHOOK_PATH=aggregate

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
