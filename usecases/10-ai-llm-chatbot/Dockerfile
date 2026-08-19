# =============================================================================
# Use Case 10 - AI / LLM Powered Chat Assistant
# -----------------------------------------------------------------------------
# Connects n8n's LangChain AI agent to a local LLM-compatible endpoint,
# exposes a webhook chat UI, answers questions from your own documents and
# calls tools (weather, MCP servers) when needed.
#
# Build:
#   docker build -t n8n-ai-chatbot .
# Run:
#   docker run -d --name n8n-ai -p 5678:5678 \
#     -v ~/.n8n:/home/node/.n8n n8n-ai-chatbot
# =============================================================================
FROM n8nio/n8n:latest

USER root

# AI agent nodes (LangChain) are built-in. MCP adds model-context-protocol tools;
# OpenWeatherMap gives the agent a live weather tool. BYO LLM API key.
RUN cd /usr/local/lib/node_modules/n8n \
    && npm install n8n-nodes-mcp n8n-nodes-openweathermap --save \
    && npm cache clean --force

# Bring your own LLM provider key (do NOT hardcode secrets in images).
ENV N8N_PROTOCOL=http \
    N8N_HOST=localhost \
    TZ=UTC \
    N8N_ENCRYPTION_KEY=CHANGE_ME_10_AI_STRONG_KEY \
    OPENAI_API_KEY=PASTE_YOUR_OWN_KEY \
    OPENWEATHER_API_KEY=PASTE_YOUR_OWN_KEY

EXPOSE 5678
VOLUME ["/home/node/.n8n"]

USER node
ENTRYPOINT ["docker-entrypoint.sh"]
