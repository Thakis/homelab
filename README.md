# homelab

> This detailed repository provides a clear representation of a robust but still beginner friendly homelab setup that balances storage, network management, and application hosting with security and efficiency.


![Homelab_20241208](https://github.com/user-attachments/assets/48d85cda-db1e-4afd-bc08-df4b4b4816fd)


> The image showcases a comprehensive homelab network and system architecture diagram, including several interconnected components, applications, and services. Below is a detailed breakdown of the different sections visible in the diagram:

### 1. **Core Infrastructure Overview**
   - **Primary Hardware**: The homelab utilizes a Synology NAS (Synology DS923+) alongside a MinisForum NAB6 for Docker containers and Virtual Machine Manager (VMM). It also integrates external storage and a Thunderbolt 4 docking station for workstation management.
   - **Network Backbone**: Currenty a Fritzbox router is the center of the network. Ethernet and wireless connections are configured for multiple devices. In the future there will be an additional UniFiSwitch.
   - **Power Supply and UPS**: A UPS (uninterruptible power supply) provides backup power and surge protection to the critical systems.

### 2. **NAS in Detail**
   - The Synology NAS acts as the central hub for data storage and backups.
   - An additional external NAS is via Tailscale connected. It serves as an external storage for the entire DS923+ system.

### 3. **MinisForum in Detail**
   - The MinisForum NAB 6 acts as the central hub for application hosting.
   - **Docker Services**: Includes various containerized applications, such as:
     - Media servers (Plex, Jellyfin, etc.).
     - File sharing and synchronization tools (e.g., Nextcloud).
     - Monitoring tools (Grafana, Prometheus).
   - **Virtual Machines**: VMM instances host additional services or operating systems for tasks like testing or isolated operations.

### 4. **Networking Components**
   - **Routing and DNS**: Local DNS resolution and network-level ad-blocking (via Pi-hole + Unbound).
   - **IoT Devices**: Managed through VLANs or dedicated network segments to enhance security.

### 5. **Workstation Setup**
   - The workstation setup connects various peripherals (e.g., monitors, printers) through a central Thunderbolt 4 docking station.
   - Laptops, desktops, and additional devices are integrated for seamless productivity.
   - **Backup Solutions**: Backups are routed to the NAS for data protection.

### 6. **Remote Access and Cloud Integration**
   - **VPN**: Secure remote access is provided using WireGuard.
   - **External Backup**: Data redundancy is maintained through services like Hyper Backup by Synology to an external NAS.
   - **Monitoring**: Tools like Grafana and Prometheus visualize system health, resource usage, and logs.

### 7. **Detailed Concepts and Diagrams**
   - The bottom portion illustrates specific network use cases and configurations, including:
     - A high-level layout of traffic routing.
     - Device interconnectivity.
     - External service interaction.

### 8. **Redundant and Emergency Systems**
   - Redundant configurations (e.g., multiple HDDs, RAID setups) are used to prevent downtime.
   - Failover setups and power protection for critical devices are included.

---




# Home Server Setup: Comprehensive Guide

## Video Tutorial Playlist

### Infrastructure and Basic Setup
1. [ApfelCast: Docker Container unter Proxmox](https://www.youtube.com/playlist)
2. [Raspberry Pi Cloud: ZERO TO HERO - Raspberry Pi Installation + Docker + Portainer](https://www.youtube.com/playlist)
3. [The Digital Life: Portainer Install Ubuntu Tutorial](https://www.youtube.com/playlist)

### Networking and Proxy
1. [Raspberry Pi Cloud: NGINX Proxy Manager - Reverse Proxy Explanation and Installation](https://www.youtube.com/playlist)
2. [Raspberry Pi Cloud: NGINX Proxy Manager - Setup and Let's Encrypt Certificates](https://www.youtube.com/playlist)
3. [ApfelCast: Nginx Proxy Manager - Reverse Proxy with Graphical Interface](https://www.youtube.com/playlist)

### Security and VPN
1. [USB Akimbo Reformed: WireGuard VPN Server with Docker](https://www.youtube.com/playlist)
2. [Andreas Spiess: Wireguard and NextCloud on Raspberry Pi](https://www.youtube.com/playlist)

### Applications and Monitoring
1. [The Digital Life: Nextcloud with Nginx Proxy Manager](https://www.youtube.com/playlist)
2. [Raspberry Pi Cloud: ZERO TO HERO - Grafana Monitoring](https://www.youtube.com/playlist)

## Recommended Setup Sequence

### 1. Infrastructure Preparation
- Choose hardware (Raspberry Pi or alternative)
- Install base operating system (Ubuntu/Raspbian)
- Set up basic network configuration

### 2. Docker Installation
- Install Docker
- Install Docker Compose
- Configure system permissions

### 3. Container Management
- Install Portainer for easy container management
- Set up user access and permissions

### 4. Networking and Security
- Install NGINX Proxy Manager
- Configure reverse proxy
- Set up Let's Encrypt SSL certificates

### 5. Essential Services
- Install WireGuard VPN
- Deploy Nextcloud
- Set up Bitwarden password manager

### 6. Monitoring and Observability
- Install Grafana
- Configure system monitoring
- Set up dashboards

## Key Tools and Services

| Service | Purpose | Docker-Friendly | Notes |
|---------|---------|-----------------|-------|
| Docker | Containerization | Yes | Core infrastructure |
| Portainer | Container Management | Yes | Graphical interface |
| NGINX Proxy Manager | Reverse Proxy | Yes | SSL and domain routing |
| WireGuard | VPN | Yes | Secure remote access |
| Nextcloud | File Sync/Share | Yes | Private cloud storage |
| Bitwarden | Password Management | Yes | Secure credential storage |
| Grafana | Monitoring | Yes | System and service metrics |

## Best Practices

- Always use strong, unique passwords
- Keep systems and containers updated
- Use Docker networks for isolation
- Implement regular backups
- Use Let's Encrypt for SSL certificates
- Monitor system resources

## Security Recommendations

- Disable root SSH login
- Use key-based authentication
- Implement fail2ban
- Regular security updates
- Use VPN for remote access
- Limit container privileges

## Troubleshooting Resources

- Docker documentation
- Portainer community forums
- NGINX Proxy Manager GitHub
- Raspberry Pi forums
- Docker compose guides

## Community and Learning

- [Docker Official Documentation](https://docs.docker.com/)
- [Portainer Documentation](https://documentation.portainer.io/)
- [NGINX Proxy Manager GitHub](https://github.com/NginxProxyManager/nginx-proxy-manager)
- Reddit communities: r/homelab, r/selfhosted

## Disclaimer

This guide is a compilation of community resources. Always test in a safe environment and understand each step before implementation.

Claude.ai was used to write the repository. Unstuckstudy.com was used to summarize YouTube videos.
