# =============================================================================
# Use Case 14 - Invoice & Payment Reminder Automation
# -----------------------------------------------------------------------------
# Tracks overdue invoices, sends a polite reminder sequence via email, escalates
# after N days and records the whole history in SQLite. Stripe community node
# confirms payments and stops reminders automatically.
#
# Build:
#   docker build -t n8n-payment-reminders .
# Run:
#   docker run -d --name n8n-reminders -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-payment-reminders
# =============================================================================
FROM n8nio/n8n:latest

USER root

# Email + Cron are built-in. Stripe checks live payment status; SQLite logs it.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-stripe n8n-nodes-sqlite --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_14_REMINDERS_STRONG_KEY \
    REMINDER_DAYS="3,7,14"

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
