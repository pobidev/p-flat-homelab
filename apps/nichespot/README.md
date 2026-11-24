# NicheSpot

Aplicación web PWA para compartir, recomendar y valorar álbumes de música entre amigos, desplegada en Docker mediante GitHub Container Registry (`ghcr.io/pobidev/nichespot`).

## Requisitos previos

- Docker y Docker Compose v2.
- Directorio de datos persistentes creado con permisos para el usuario del contenedor (`2100:988`):

```bash
sudo mkdir -p /srv/homelab/nichespot/data
sudo chown -R 2100:988 /srv/homelab/nichespot/data