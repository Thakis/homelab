# Proxmox - Disable License Notification

## Overview
This guide explains how to remove the persistent license notification in Proxmox Virtual Environment (VE).

## Resources
- Video Tutorial: [Proxmox License Information Disable [4K | DE]](https://youtu.be/zuP8xJLaXFk?si=5LYfZnKgPRG3UftI)
- Additional Reference: [Hoerli.net - Proxmox License Disable Guide](https://hoerli.net/proxmox-lizenzinformation-abschalten/)

## Method to Disable License Notification

### 1. SSH into Proxmox Server
```bash
ssh root@your-proxmox-ip
```

### 2. Edit Proxmox Web Interface JavaScript
Open the following file:
```bash
nano /usr/share/perl5/Proxmox/API2/Nodes.pm
```

### 3. Modify the Notification Logic
Find and comment out or remove the license check logic.

### 4. Restart Proxmox Web Service
```bash
systemctl restart pveproxy
```

## Important Notes
- This method is for home/lab use
- Always keep your Proxmox installation updated
- Consider purchasing a subscription for production environments
- Proceed at your own risk

## Disclaimer
- This guide is for educational purposes
- Modifying system files can impact system stability
- Backup your configuration before making changes

## Alternative Options
1. Purchase a Proxmox subscription
2. Use the free Community Edition
3. Temporarily ignore the notification