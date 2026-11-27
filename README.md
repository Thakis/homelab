# Homelab Documentation

> A clean, privacy-focused, and beginner-friendly homelab setup balancing reliable storage, network security, and self-hosted services.

<img width="3862" height="5546" alt="Homelab Architecture Diagram" src="https://github.com/user-attachments/assets/052a6cd9-1031-43c8-a12b-63f09b23a2e1" />

---

## 📑 Table of Contents
- [Hardware Overview](#-hardware-overview)
- [Network & Security](#-network--security)
- [Services & Applications](#-services--applications)
- [Backup Strategy](#-backup-strategy)
- [Repository Structure](#-repository-structure)

---

## 🖥️ Hardware Overview

| Device | Role | Key Components / Notes |
| :--- | :--- | :--- |
| **MinisForum NAB6** | Compute & Application Host | Runs Proxmox VE (VMs & LXC) and Docker containers |
| **Synology DS923+** | Primary NAS & Storage | Central data hub, RAID redundancy, Hyper Backup |
| **Raspberry Pi** | Network & Utility Node | Local DNS (Pi-hole + Unbound), Tailscale, NFS backups |
| **External NAS** | Off-site Backup Target | Connected securely via Tailscale |
| **FRITZ!Box** | Router & Gateway | Main internet gateway *(UniFi Switch planned for future)* |
| **UPS** | Power Protection | Backup power & surge protection for critical hardware |

---

## 🔒 Network & Security

- **DNS & Ad-Blocking:** Local DNS resolution and network-wide ad-blocking using **Pi-hole + Unbound**.
- **Remote Access:** Secure VPN access via **WireGuard** (personal devices) and **Tailscale** (site-to-site / off-site NAS connection).
- **Segmentation:** Dedicated network segments / VLANs for IoT devices to isolate them from the core network.
- **Reverse Proxy & SSL:** Managed access to internal services with SSL encryption.

---

## 🚀 Services & Applications

* **Media:** Jellyfin / Plex
* **Cloud & Productivity:** Nextcloud
* **Password Management:** Vaultwarden / Bitwarden
* **Monitoring & Observability:** Grafana, Prometheus
* **Container Management:** Docker, Docker Compose, Portainer

*(Note: All sensitive configurations, IPs, and credentials are omitted from this repository for security reasons.)*

---

## 💾 Backup Strategy

- **Local Redundancy:** RAID configuration on the Synology DS923+ to protect against drive failures.
- **Automated Backups:** Workstation and server backups routed to the primary NAS.
- **Off-site Backup:** Encrypted backups via **Synology Hyper Backup** to an external NAS connected over Tailscale.

---

## 📂 Repository Structure

Detailed setup notes and configurations are organized by host:

- [`NAB6/`](./NAB6) – Proxmox setup, SSH containers, and application hosting notes
- [`RaspberryPi/`](./RaspberryPi) – Pi-hole, Unbound, Tailscale, and NFS backup configurations
- [`Synology DS923+/`](./Synology%20DS923+/) – NAS setup and backup documentation

---

## 📝 Disclaimer

This repository documents my personal homelab setup for educational purposes and inspiration. Always test configurations in a safe environment before applying them to your own network.
