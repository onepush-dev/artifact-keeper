# Artifact Keeper web UI on Railway: the official ghcr.io/artifact-keeper/artifact-keeper-web:1.12.1 image (MIT),
# application unmodified. Railway layer: HTTPS mode on (Railway serves every domain over TLS), so the UI sends
# HSTS and upgrade-insecure-requests. Railway's injected PORT (8080) is what the server listens on.
FROM ghcr.io/artifact-keeper/artifact-keeper-web:1.12.1
LABEL org.opencontainers.image.source="https://github.com/onepush-dev/artifact-keeper"
ENV AK_ENFORCE_HTTPS=true \
    PORT=8080
EXPOSE 8080
