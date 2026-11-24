# Artifact Keeper on Railway

[Artifact Keeper](https://github.com/artifact-keeper/artifact-keeper) (MIT): a self-hosted universal artifact registry for Docker/OCI images, npm, PyPI, Maven, Cargo, Helm, Go, NuGet and 40+ other package formats, with proxies, virtual repositories, tokens and audit. An open-source alternative to Artifactory and Nexus. Deploy it on Railway with one click.

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/deploy/TEMPLATE_CODE)

## What this template runs
| Service | Image | Role |
|---|---|---|
| **artifact-keeper** (public) | `ghcr.io/onepush-dev/artifact-keeper-proxy:1.12.4` (Caddy 2.11.9 + upstream's Caddyfile routes) | Listens on 8080. `/api`, `/health`, `/livez`, `/readyz`, `/v2` (OCI) and every package-format prefix (`/npm`, `/pypi`, `/maven`, `/cargo`, `/helm`, …) go to the backend; everything else goes to the web UI. |
| **backend** (private) | `ghcr.io/onepush-dev/artifact-keeper-backend:1.12.4` (official backend image, app unmodified; runs as root for the volume) | Rust API on 8080. Volume `/data` holds storage, backups, plugins and the scan workspace. |
| **web** (private) | `ghcr.io/artifact-keeper/artifact-keeper-web:1.12.1` (official) | Next.js UI. |
| **Postgres** | Railway Postgres | Metadata (repositories, artifacts, users, tokens). |

Upstream's optional OpenSearch, Trivy, OpenSCAP and Dependency-Track services are not included; add them later if you want search indexing and vulnerability scanning.

## Variables
| Service | Variable | Value |
|---|---|---|
| backend | `DATABASE_URL` | `${{Postgres.DATABASE_URL}}` |
| backend | `JWT_SECRET` | `${{secret(64)}}` |
| backend | `ADMIN_PASSWORD` | generated per deploy; password of the built-in `admin` account (applied when the account is first created) |
| backend | `AK_WEBHOOK_SECRET_KEY` | generated 32-byte base64 key that encrypts webhook signing secrets |
| backend | `CORS_ORIGINS` | `https://${{artifact-keeper.RAILWAY_PUBLIC_DOMAIN}}` |
| web | `BACKEND_URL` | `http://${{backend.RAILWAY_PRIVATE_DOMAIN}}:8080` |

## After deploy
Open the public URL and sign in as `admin` with the `ADMIN_PASSWORD` value from the backend service's Variables tab. Create repositories, then point clients at `https://<your-domain>/npm/<repo>/`, `https://<your-domain>/pypi/<repo>/simple/`, `docker login <your-domain>` and so on (see the docs: https://artifactkeeper.com/docs/).

Not affiliated with the Artifact Keeper project. "JFrog" and "Artifactory" are trademarks of JFrog Ltd.
