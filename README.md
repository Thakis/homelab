# homelab

> This detailed repository provides a clear representation of a robust but still beginner friendly homelab setup that balances storage, network management, and application hosting with security and efficiency.


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
     - Network utilities (Pi-hole + Unbound for DNS filtering).
     - Monitoring tools (Grafana, Prometheus).
   - **Virtual Machines**: A VMM instance hosts additional services or operating systems for tasks like testing or isolated operations.

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