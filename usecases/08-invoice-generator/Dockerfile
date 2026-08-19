# =============================================================================
# Use Case 08 - PDF Invoice Generator & Delivery
# -----------------------------------------------------------------------------
# Turns order data into branded PDF invoices, stores them in MongoDB as an
# archive, emails them to customers and logs delivery status.
#
# Build:
#   docker build -t n8n-invoice-generator .
# Run:
#   docker run -d --name n8n-invoice -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-invoice-generator
# =============================================================================
FROM n8nio/n8n:latest

USER root

# PDF generation + email delivery are built-in. MongoDB archives invoices.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-mongodb --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_08_INVOICE_STRONG_KEY \
    MONGODB_URI=mongodb://localhost:27017 \
    MONGODB_DATABASE=n8n_invoices

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
