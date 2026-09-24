# Seerr

Seerr is deployed as a Docker Compose service inside the Docker VM. It is used as the request management frontend for the media stack, allowing users to request movies and series that are later handled by Radarr and Sonarr.

The service runs with the same shared media user as the rest of the multimedia stack, using UID/GID `2000:2000`. Persistent application data is stored on the VM local disk, while the media library itself remains on the NAS and is managed by the other services in the stack.

## Requirements

- Docker Engine
- Docker Compose plugin
- Shared Docker network with Jellyfin, Radarr and Sonarr
- `media:media` using UID/GID `2000:2000`
- Existing Jellyfin, Radarr and Sonarr instances already working

## Deploy

```bash
cp .env.example .env
# Edit .env for the local machine

docker compose --env-file .env -f compose.yaml config
docker compose --env-file .env -f compose.yaml up -d
```

## Verify

```bash
docker compose --env-file .env -f compose.yaml ps
docker compose --env-file .env -f compose.yaml logs --tail=100 seerr
curl -I http://localhost:5055
```

## Storage

| Purpose | Host path | Container path |
|---|---|---|
| Configuration | `/srv/homelab/arr-stack/seerr/config` | `/app/config` |

## Network

Seerr must be attached to the same Docker network as Jellyfin, Radarr and Sonarr so it can resolve them by service name.

Expected service endpoints inside Docker:

| Service | URL |
|---|---|
| Jellyfin | `http://jellyfin:8096` |
| Radarr | `http://radarr:7878` |
| Sonarr | `http://sonarr:8989` |

## Initial configuration

After the first start, access Seerr from the browser:

```text
http://IP_DE_LA_VM:5055
```

During the setup wizard, configure:

- Jellyfin URL: `http://jellyfin:8096`
- Radarr URL: `http://radarr:7878`
- Sonarr URL: `http://sonarr:8989`

The following values must be taken from the running services:

- Radarr API key
- Sonarr API key
- Quality profiles
- Root folders

Root folders must use the internal paths expected by Radarr and Sonarr, not the host paths.

Examples:

```text
/data/pelis
/data/series
```

## Important

Seerr does not manage media files directly. It only coordinates requests and sends them to Radarr and Sonarr.

The service should stay on the internal Docker network and should not be exposed publicly without proper protection such as VPN, reverse proxy hardening, or equivalent access control.