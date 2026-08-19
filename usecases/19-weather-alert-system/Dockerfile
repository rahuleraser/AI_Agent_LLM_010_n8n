# =============================================================================
# Use Case 19 - Weather Alerts & Smart Notifications
# -----------------------------------------------------------------------------
# Polls OpenWeatherMap for your city on a schedule, compares against
# thresholds and sends rain/heat/storm alerts to Telegram, email or Discord.
#
# Build:
#   docker build -t n8n-weather-alerts .
# Run:
#   docker run -d --name n8n-weather -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-weather-alerts
# =============================================================================
FROM n8nio/n8n:latest

USER root

# OpenWeatherMap community node wraps the weather API into a ready node.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-openweathermap n8n-nodes-telegram --save \
    && npm cache clean --force

ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_19_WEATHER_STRONG_KEY \
    WEATHER_CITY=London \
    WEATHER_POLL_MINUTES=30

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
