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


## 5. Argon One Raspberry Pi Case Configuration

## Installation

To install the Argon One case software, run the following command:

```bash
curl https://download.argon40.com/argon1.sh | bash
```

## Configuration Commands

- `argonone-config` → Configure fan settings
- `argonone-uninstall` → Uninstall Argon One software

## Customizing Fan Control

Edit the fan configuration file:

```bash
sudo nano /etc/argononed.conf
```

### Sample Fan Configuration

In the configuration file, you can set fan speeds based on temperature:

```
55=10    # At 55°C, set fan to 10% speed
60=55    # At 60°C, set fan to 55% speed
65=100   # At 65°C, set fan to 100% speed
```

After modifying the configuration, restart the service:

```bash
sudo systemctl restart argononed.service
```

## Reference

- Original configuration guide: [Argon One Case PDF](https://www.helmuthinterthuer.de/images/download/argon_one_case.pdf)

## Notes

- Ensure you have appropriate cooling for your Raspberry Pi
- Adjust temperature and fan speed values according to your specific needs and environment



## 6. Install Docker
```bash
apt install curl
sudo curl -sSL https://get.docker.com | sh
apt install docker-compose -y
```

## 7. Install Portainer
Follow official documentation: [Portainer Installation Guide](https://docs.portainer.io/start/install-ce/server/docker/linux)

## 8. Install Nginx Proxy Manager
- Change Portainer app templates to: `https://raw.githubusercontent.com/pi-hosted/pi-hosted/master/template/portainer-v2-amd64.json`
- Choose "Nginx Proxy Manager v2 with Sqllite"
- Default Administrator:
  - Email: `admin@example.com`
  - Password: `changeme`
Reference: [Nginx Proxy Manager Video Guide](https://www.youtube.com/watch?v=0_lgbiw1TNs)

## 9. Install Tarpit
```bash
docker container run -d --name endlessh -p 22:2222 harshavardhanj/endlessh:latest
```

## 10. Install Heimdall
```bash
# Ports mapping
# 4432:80
# 8020:443
```

## 11. Install Gotify
```bash
docker run -p 8050:80 -e TZ="Europe/Berlin" -v /var/gotify/data:/app/data ghcr.io/gotify/server-arm64
```
Official documentation: [Gotify Install Guide](https://gotify.net/docs/install)

## 12. Install Watchtower
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

## 13. Install Pi-hole + Unbound
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


## 14. Tailscale Installation on Raspbian Bookworm

### Video Tutorial
[Tailscale Installation Guide](https://www.youtube.com/watch?v=YTjYXii4WzI)

### Installation Steps

#### 1. Add Tailscale's GPG Key
```bash
sudo mkdir -p --mode=0755 /usr/share/keyrings
curl -fsSL https://pkgs.tailscale.com/stable/raspbian/bookworm.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
```

#### 2. Add Tailscale Repository
```bash
curl -fsSL https://pkgs.tailscale.com/stable/raspbian/bookworm.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

#### 3. Install Tailscale
```bash
sudo apt-get update && sudo apt-get install tailscale
```

#### 4. Start Tailscale
```bash
sudo tailscale up
```

### What Each Step Does

- **Add GPG Key**: Adds the official Tailscale repository key to verify package authenticity
- **Add Repository**: Configures the Tailscale package repository for Raspbian Bookworm
- **Install Tailscale**: Updates package lists and installs Tailscale
- **Start Tailscale**: Initiates the Tailscale connection and begins authentication

### Post-Installation

- You will be prompted to log in to your Tailscale account
- Follow the authentication instructions in the terminal or via the provided URL

### Official Resources

- [Tailscale Raspbian Packages](https://pkgs.tailscale.com/stable/#raspbian-bookworm)
- [Tailscale Documentation](https://tailscale.com/kb/installation)

### Notes

- Ensure you have an active internet connection
- Requires sudo privileges
- Compatible with Raspbian Bookworm