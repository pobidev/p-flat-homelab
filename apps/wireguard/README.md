# Wireguard

Wireguard is deployed as a Docker Compose service inside the Docker VM. Its function is to make a tunnel to manage the server from outside your network.

## Requirements

- Docker Engine
- Docker Compose plugin

## Deploy

```bash
cp .env.example .env
# Edit .env for the local machine

docker compose config
docker compose up -d
```

## Verify
First, you shoud verify that the image is running.

```bash
docker compose ps
```

Then, connect any peer and check that it shows "latest hadnshake: x seconds ago" when executing this command in the peer.

```bash
sudo wg show
```

Or this one in the server.

```bash
docker exec wireguard wg show
```
## Important

Wireguard generates a qr for each peer, if you want to connect to the vpn using your phone it's preatty convenient.