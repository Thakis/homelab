# Study Guide: Installing Jellyfin Media Server on Proxmox

## Video Reference
- [Proxmox HomeServer Teil 30 - Installation von Jellyfin Media Server](https://www.youtube.com/watch?v=VMfz_1Kd-jk&list=PLRcp6YbTf6Qk3pIZnrKBTEJ8lQl5NZujz)

## Overview
This guide provides a comprehensive step-by-step process for installing the Jellyfin Media Server on a Proxmox environment. Jellyfin allows you to centralize your media library, making it accessible from various devices over your network.

## Prerequisites
- Proxmox server set up and running
- Basic knowledge of Linux commands
- Access to a NAS (Network Attached Storage) for storing media files

## Step-by-Step Installation

### 1. Create a New Container
1. Access Proxmox and log into your server
2. Create a new container:
   - Assign a unique container ID and hostname
   - Set a strong password
   - **Important:** Ensure it is a privileged container (uncheck the unprivileged container option)

### 2. Configure Container Settings
- **Template:** Ubuntu 22.04
- **Disk Size:** 8 GB (media files will be stored on NAS)
- **CPU and Memory:** 
  - Start with 2 CPU cores 
  - Allocate 2 GB RAM (adjust based on usage)
- **Network:** Assign a static IP address

### 3. Update the Container
Access the container console and run:
```bash
apt-get update
apt-get upgrade -y
apt-get autoremove
```

### 4. Install Required Packages
Create a mount point for NAS:
```bash
mkdir /mnt/jellyfin
apt-get install cifs-utils
```

### 5. Configure NAS Connection
Edit the fstab file:
```bash
nano /etc/fstab
```
Add the following line (replace placeholders):
```
//<NAS_IP>/home /mnt/jellyfin cifs username=<username>,password=<password>,uid=1000,gid=1000 0 0
```

### 6. Mount the NAS
```bash
mount -a
```

### 7. Install Jellyfin
Install dependencies and Jellyfin:
```bash
apt-get install sudo curl
curl https://repo.jellyfin.org/install-debuntu.sh | sudo bash
```

### 8. Access and Configure Jellyfin
1. Verify Jellyfin service:
   ```bash
   systemctl status jellyfin
   ```
2. Open web interface:
   - Navigate to `http://<Container_IP>:8096`
   - Complete initial setup
   - Add media library directories

## Troubleshooting Tips
- Ensure NAS credentials are correct
- Check network connectivity
- Verify Jellyfin service is running
- Consult [Jellyfin Documentation](https://jellyfin.org/docs/) for advanced configuration

## Conclusion
You've now successfully set up a Jellyfin Media Server on your Proxmox server, enabling media streaming across your devices.

## Additional Resources
- [Jellyfin Official Website](https://jellyfin.org/)
- [Jellyfin GitHub Repository](https://github.com/jellyfin/jellyfin)

## Disclaimer
- Always backup your data before making system changes
- Adjust resources as needed based on your specific usage and hardware

## Need Help?
Join the Jellyfin community forums or reach out to support channels for assistance with specific issues.
