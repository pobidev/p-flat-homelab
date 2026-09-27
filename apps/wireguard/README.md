# Jellyfin

Jellyfin is deployed as a Docker Compose service inside the Docker VM. It uses the user "Media", shared between this container and every other container that manages the media library, mainly the *Arr Stack and Torrent. The media files are stored externally on a NAS, sharing its files via NFS.

## Requirements

- Docker Engine
- Docker Compose plugin
- NFS mounted on the VM
- `media:media` using UID/GID `2000:2000`

## Deploy

```bash
cp .env.example .env
# Edit .env for the local machine

docker compose config
docker compose up -d
```

## Verify

```bash
docker compose ps
docker compose logs --tail=100 jellyfin
curl -I http://localhost:8096
```

## Storage

| Purpose | Host path | Container path |
|---|---|---|
| Configuration | `/srv/.../config` | `/config` |
| Cache | `/srv/.../cache` | `/cache` |
| Movies | `/mnt/.../pelis` | `/media/pelis` |
| Series | `/mnt/.../series` | `/media/series` |

## Important

The media paths are mounted read-write because Jellyfin is intentionally allowed to delete media from its interface. Configuration and cache remain on the VM's local disk.