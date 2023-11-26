# docker-mods

Collection of mod for linuxserver.io docker containers.

Based on [jordanpotter/docker-mods](https://github.com/jordanpotter/docker-mods).

## Available mods

### transmission-gluetun-port-update

Updates the port in the transmission configuration to match the port forwarding set by gluetun.

#### Usage

```yaml
version: "3.8"

services:
  wireguard:
    image: ghcr.io/qdm12/gluetun
    container_name: wireguard
    restart: always
  transmission:
    image: lscr.io/linuxserver/transmission:latest
    container_name: transmission
    restart: always
    network_mode: "service:wireguard"
    environment:
      - DOCKER_MODS=michsior14/docker-mods:transmission-gluetun-port-update # or michaukrieg/docker-mods:transmission-gluetun-port-update
      ## Other environment variables e.g
      #- GLUETUN_PORT=8080
```

Supported environment variables can be checked [here](https://github.com/Michsior14/transmission-gluetun-port-update?tab=readme-ov-file#available-environment-variables). Note that `TRANSMISSION_USER` and `TRANSMISSION_PASSWORD` are set automatically based on main image configuration.
