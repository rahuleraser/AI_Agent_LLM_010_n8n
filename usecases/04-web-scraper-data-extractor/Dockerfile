# =============================================================================
# Use Case 04 - Web Scraper & Data Extraction
# -----------------------------------------------------------------------------
# Scrapes public product/price pages on a schedule, normalizes the HTML,
# detects price drops and stores results locally. Uses built-in HTTP Request,
# HTML Extract, Cron and Filter nodes.
#
# Build:
#   docker build -t n8n-web-scraper .
# Run:
#   docker run -d --name n8n-scraper -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-web-scraper
# =============================================================================
FROM n8nio/n8n:latest

USER root

# Scraper uses built-in HTTP Request + HTML Extract nodes. A community
# headless-browser node can be added for JavaScript-heavy pages:
# RUN cd /usr/local/lib/node_modules/n8n \
#     && npm install n8n-nodes-mcp --save \
#     && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_04_SCRAPER_STRONG_KEY \
    SCRAPE_INTERVAL_MINUTES=60

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
