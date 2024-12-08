# Raspberry Pi Ultimate Setup Guide

## 1. Install Raspberry Pi OS
- Download and install from: [Raspberry Pi Official Software](https://www.raspberrypi.com/software/)

## 2. Set Fixed DNS
Edit `/etc/resolv.conf` and add:
```
nameserver 1.1.1.2
nameserver 1.0.0.2
```
More details: [Change DNS Server Guide](https://learnubuntu.com/change-dns-server/)

## 3. System Update
```bash
apt-get update && apt-get upgrade -y && apt autoremove -y
```

## 4. Secure SSH Server
Edit SSH configuration:
```bash
nano /etc/ssh/sshd_config
```
Modify these lines:
- `PermitRootLogin No`
- Change SSH port to `65437`

Restart SSH service:
```bash
/etc/init.d/ssh restart
```
Reference: [SSH Security Video Guide](https://www.youtube.com/watch?v=64XS0HzoS_U)

## 5. Install Docker
```bash
apt install curl
sudo curl -sSL https://get.docker.com | sh
apt install docker-compose -y
```

## 6. Install Portainer
Follow official documentation: [Portainer Installation Guide](https://docs.portainer.io/start/install-ce/server/docker/linux)

## 7. Install Nginx Proxy Manager
- Change Portainer app templates to: `https://raw.githubusercontent.com/pi-hosted/pi-hosted/master/template/portainer-v2-amd64.json`
- Choose "Nginx Proxy Manager v2 with Sqllite"
- Default Administrator:
  - Email: `admin@example.com`
  - Password: `changeme`
Reference: [Nginx Proxy Manager Video Guide](https://www.youtube.com/watch?v=0_lgbiw1TNs)

## 8. Install Tarpit
```bash
docker container run -d --name endlessh -p 22:2222 harshavardhanj/endlessh:latest
```

## 9. Install Heimdall
```bash
# Ports mapping
# 4432:80
# 8020:443
```

## 10. Install Gotify
```bash
docker run -p 8050:80 -e TZ="Europe/Berlin" -v /var/gotify/data:/app/data ghcr.io/gotify/server-arm64
```
Official documentation: [Gotify Install Guide](https://gotify.net/docs/install)

## 11. Install Watchtower
```bash
docker run -it -d \
  --name watchtower \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -e WATCHTOWER_NOTIFICATIONS=gotify \
  -e WATCHTOWER_NOTIFICATION_GOTIFY_URL="http://192.168.178.25:8050" \
  -e WATCHTOWER_NOTIFICATION_GOTIFY_TOKEN="AWP-4e29yKkHzz4" \
  containrrr/watchtower:latest \
  --cleanup \
  --include-restarting \
  --rolling-restart \
  --include-stopped \
  --schedule "0 0 2 * **"
```

## 12. Install Pi-hole + Unbound
- Use Docker template: "Pi-Hole-Unbound"
- Repository: [Docker Pi-Hole Unbound](https://github.com/chriscrowe/docker-pihole-unbound/tree/main/one-container)

### Additional Pi-hole Resources
- Full Guide: [RPiList Pi-Hole Guide](https://github.com/RPiList/specials/tree/master/Anleitungen)
- Blocklists:
  - [RPiList Blocklists Overview](https://github.com/RPiList/specials/tree/master/Blocklisten)
  - [Detailed Blocklists](https://github.com/RPiList/specials/blob/master/Blocklisten.md)

## Notes
- Always ensure you have backups before making system changes
- Modify default passwords and tokens
- Keep your system and containers updated
