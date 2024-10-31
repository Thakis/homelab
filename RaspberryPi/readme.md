1. Install raspberry Pi OS
https://www.raspberrypi.com/software/

2. set fix DNS
https://learnubuntu.com/change-dns-server/
# nameserver 1.1.1.2
# nameserver 1.0.0.2

3. update
apt-get update && apt-get upgrade -y && apt autoremove -y

4. change SSH Port
# protect SSH Server - Root Zugriff verweigern + change Port: https://www.youtube.com/watch?v=64XS0HzoS_U
nano /etc/ssh/sshd_config
PermitRootLogin No
Port <> 65437
# Strg+o Enter Strg+c
/etc/init.d/ssh restart

5. install docker
apt install curl sudo
curl -sSL https://get.docker.com | sh
apt install docker-compose -y

6. install portainer
https://docs.portainer.io/start/install-ce/server/docker/linux

7. install nginx proxy manager
- https://www.youtube.com/watch?v=0_lgbiw1TNs
- change app templates in portainer to https://raw.githubusercontent.com/pi-hosted/pi-hosted/master/template/portainer-v2-amd64.json
- choose "Nginx Proxy Manager v2 with Sqllite" and install
# Default Administrator
# UserEmail:    admin@example.com
# Password: changeme

8. install tarpit
$ docker container run -d --name endlessh -p 22:2222 \
harshavardhanj/endlessh:latest

9. install heimdall
App template
# 4432:80
# 8020:443

10. install gotify
https://gotify.net/docs/install
# docker run -p 8050:80 -e TZ="Europe/Berlin" -v /var/gotify/data:/app/data ghcr.io/gotify/server-arm64


11. install watchtower
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
	--schedule "0 0 2 * * *"


12. install pihole + Unbound
- Template "Pi-Hole-Unbound"
https://github.com/chriscrowe/docker-pihole-unbound/tree/main/one-container
- Full Guide PiHole: https://github.com/RPiList/specials/tree/master/Anleitungen
- Blocklisten: https://github.com/RPiList/specials/tree/master/Blocklisten
-- https://github.com/RPiList/specials/blob/master/Blocklisten.md