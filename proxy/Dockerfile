# Artifact Keeper edge proxy on Railway: caddy:2.11.9-alpine with upstream's Caddyfile routes (v1.12.4), listening on
# 8080 and forwarding to the backend and web services over Railway's private network.
FROM caddy:2.11.9-alpine
LABEL org.opencontainers.image.source="https://github.com/onepush-dev/artifact-keeper"
COPY Caddyfile /etc/caddy/Caddyfile
ENV AK_BACKEND_UPSTREAM=backend.railway.internal:8080 \
    AK_WEB_UPSTREAM=web.railway.internal:8080
EXPOSE 8080
CMD ["caddy", "run", "--config", "/etc/caddy/Caddyfile", "--adapter", "caddyfile"]
