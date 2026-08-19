# =============================================================================
# Use Case 12 - Sales Analytics & BI Pipeline
# -----------------------------------------------------------------------------
# Aggregates sales data from multiple sources (CRM, e-commerce, payments) on a
# schedule, cleans and transforms it, then writes it to PostgreSQL/Baserow for
# dashboards and sends a weekly KPI digest.
#
# Build:
#   docker build -t n8n-sales-pipeline .
# Run:
#   docker run -d --name n8n-sales -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-sales-pipeline
# =============================================================================
FROM n8nio/n8n:latest

USER root

# Postgres, HTTP and aggregate/transform nodes are built-in. Baserow acts as
# the self-hosted analytics warehouse.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-baserow --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_12_SALES_STRONG_KEY \
    POSTGRES_HOST=localhost \
    POSTGRES_DATABASE=analytics

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
