# Arr Stack

The Arr Stack is deployed as a Docker Compose stack inside the Docker VM. It groups together the services responsible for indexers, download management, request handling, and media acquisition workflows.

This stack is built around a shared service user, `media:media`, using UID/GID `2000:2000`. Persistent application data is stored on the VM local disk, while the actual media library lives on the NAS and is mounted into the containers through the VM.

## Services

The stack currently includes, or is expected to include, the following services:

- qBittorrent
- Sonarr
- Radarr
- Prowlarr
- Bazarr
- FlareSolverr
- Seerr

## Requirements

- Docker Engine
- Docker Compose plugin
- NAS mounted on the VM
- Shared media user `media:media` using UID/GID `2000:2000`
- Valid `.env` file adapted to the machine
- Existing storage paths under `/srv/homelab/arr-stack`
- Existing media paths under `/mnt/NAS/media`

## Deploy

```bash
cp .env.example .env
# Edit .env for the local machine

docker compose --env-file .env config
docker compose --env-file .env up -d
```

## Verify

```bash
docker compose --env-file .env ps
docker compose --env-file .env logs --tail=100
```

## Storage

| Purpose | Host path | Container path |
|---|---|---|
| Stack root | `/srv/homelab/arr-stack` | varies by service |
| Media root | `/mnt/NAS/media` | `/data` or service-specific mounts |
| Seerr config | `/srv/homelab/arr-stack/seerr/config` | `/app/config` |
| qBittorrent config | `/srv/homelab/arr-stack/qbittorrent/config` | service-defined |
| Sonarr config | `/srv/homelab/arr-stack/sonarr/config` | service-defined |
| Radarr config | `/srv/homelab/arr-stack/radarr/config` | service-defined |
| Prowlarr config | `/srv/homelab/arr-stack/prowlarr/config` | service-defined |
| Bazarr config | `/srv/homelab/arr-stack/bazarr/config` | service-defined |

## Environment

The stack uses a shared `.env` with a small set of common variables.

Example:

```env
PUID=2000
PGID=2000
TZ=Europe/Madrid

STACK_ROOT=/srv/homelab/arr-stack
DATA_ROOT=/mnt/NAS/media

QBITTORRENT_WEBUI_PORT=8090
QBITTORRENT_TORRENT_PORT=51506
SONARR_PORT=8989
RADARR_PORT=7878
PROWLARR_PORT=9696
BAZARR_PORT=6767
FLARESOLVERR_PORT=8191
SEERR_PORT=5055
```

## Important

All services should use the same UID/GID when they need shared access to downloads and media files. This helps keep permissions predictable and avoids using unsafe permission workarounds.

Services should communicate through Docker service names on a shared internal network instead of relying on fixed container IPs.