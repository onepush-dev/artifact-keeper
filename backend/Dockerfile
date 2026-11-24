# Artifact Keeper backend on Railway: the official ghcr.io/artifact-keeper/artifact-keeper-backend:1.12.4 image
# (MIT), application unmodified. Railway layer: runs as root so it can write the Railway volume mounted at /data
# (Railway volumes are root-owned), keeps storage, backups, plugins and the scan workspace on that one volume, and
# trusts Railway's private proxy range for client IPs.
FROM ghcr.io/artifact-keeper/artifact-keeper-backend:1.12.4
LABEL org.opencontainers.image.source="https://github.com/onepush-dev/artifact-keeper"
USER 0
ENV HOST=0.0.0.0 \
    ENVIRONMENT=production \
    STORAGE_PATH=/data/storage \
    BACKUP_PATH=/data/backups \
    PLUGINS_DIR=/data/plugins \
    SCAN_WORKSPACE_PATH=/data/scan-workspace \
    RATE_LIMIT_TRUSTED_PROXY_CIDRS=100.64.0.0/10 \
    RUST_LOG=info \
    LOG_FORMAT=text
EXPOSE 8080
