# P-Flat-Homelab
Personal project focused on learning how to automate and manage a personal homelab server.

My current objective is to migrate the current setup I have, (mainly LXC containers running a media stack, with services like Jellyfin, the *arr suite, and NginxPM, among other small stuff) to a functional Docker focused workflow. Besides, I will add monitoring and networking apps.

As I work on it, I will add diary entries or something along those lines to the documents. I will grind at it while I study, so progress will be slow and moderate. I'd rather learn slowly than rush it all at first.

## Goals

- Learn Docker and Compose through real services.
- Practice Linux administration and networking.
- Build monitoring and alerting.
- Automate backups and deployments.
- Document operational decisions.
- Create an interview-ready DevOps/SRE portfolio project.

## Architecture

```text
NAS / OpenMediaVault
        |
        | NFS
        v
Proxmox
        |
        v
Docker VM
        |
        +-- Jellyfin
        +-- *arr stack
        +-- Reverse proxy
        +-- Prometheus
        +-- Grafana
```

## Current status

- [x] Proxmox VM created for Docker
- [x] NFS mounted directly inside the Docker VM
- [x] Jellyfin deployed with Docker Compose
- [x] Jellyfin users and watch history migrated
- [ ] Deploy Sonarr/Radarr/Prowlarr
- [ ] Add reverse proxy
- [ ] Add monitoring
- [ ] Add automated backups
- [ ] Add CI validation
- [ ] Add VPN
- [ ] Publish architecture diagrams

## Technologies

- Proxmox
- Linux
- Docker
- Docker Compose
- OpenMediaVault
- NFS
- Jellyfin
- Prometheus
- Grafana
- GitHub Actions

## Documentation

- [Operations diary](docs/diary/)
- [Architecture diagrams](docs/diagrams/)