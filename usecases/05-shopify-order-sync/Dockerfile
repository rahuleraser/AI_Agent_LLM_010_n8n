# =============================================================================
# Use Case 05 - E-commerce Order Sync (Shopify to Google Sheets)
# -----------------------------------------------------------------------------
# Watches Shopify for new orders, enriches them with customer data and syncs
# them to Google Sheets + a local SQLite mirror. Stripe community node added
# for payment reconciliation.
#
# Build:
#   docker build -t n8n-shopify-order-sync .
# Run:
#   docker run -d --name n8n-shopify -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-shopify-order-sync
# =============================================================================
FROM n8nio/n8n:latest

USER root

# Shopify is built-in. Add Stripe for payment/refund reconciliation.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-stripe --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_05_SHOPIFY_STRONG_KEY \
    SHOPIFY_STORE_URL=your-store.myshopify.com

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
