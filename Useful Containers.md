# Uptime Kuma
Source: https://uptime.kuma.pet/
Uptime Kuma can be used to monitor specified web services and notify in case of a offline service.
Exemplary Docker Compose file:
```
# Simple docker-compose.yml
# You can change your port or volume location

version: '3.3'

services:
  uptime-kuma:
    image: louislam/uptime-kuma:1
    container_name: uptime-kuma
    volumes:
      - /var/lib/docker/volumes/uptime-kuma-data:/app/data
    ports:
      - 3001:3001  # <Host Port>:<Container Port>
    restart: always
```

# Heimdall
Source: https://github.com/linuxserver/Heimdall
Heimdall can be used to create a browser dashboard with specified apps or webservices as shortcuts.