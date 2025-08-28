## Docker
### docker-compose.yml
```
name: tailscale
services:
  tailscale:
    container_name: tailscale
    restart: unless-stopped
    cap_add:
      - NET_ADMIN
    environment:
      - TS_USERSPACE=true
      - TS_SOCKS5_SERVER=0.0.0.0:1055
    ports:
      - 127.0.0.1:1055:1055
    volumes:
      - /var/www/tailscale-socks5:/var/lib/tailscale
    image: tailscale/tailscale:latest
    command: tailscaled --tun=userspace-networking --socks5-server=0.0.0.0:1055
```

## Package


