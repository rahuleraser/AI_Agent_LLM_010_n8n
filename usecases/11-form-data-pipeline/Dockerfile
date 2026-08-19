# =============================================================================
# Use Case 11 - Web Form Data Pipeline (Forms to Sheets/Base)
# -----------------------------------------------------------------------------
# Receives submissions from Google Forms / Typeform webhooks, validates fields,
# writes rows to Google Sheets, stores originals in Baserow and sends a
# confirmation email.
#
# Build:
#   docker build -t n8n-form-pipeline .
# Run:
#   docker run -d --name n8n-forms -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-form-pipeline
# =============================================================================
FROM n8nio/n8n:latest

USER root

# Google Sheets is built-in. Baserow gives you a free self-hosted database UI.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-baserow --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_11_FORM_STRONG_KEY \
    FORM_WEBHOOK_PATH=form-submit

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
