# Study Guide for Proxmox Windows 11 Installation

## Video Tutorial
[Proxmox HomeServer Teil 15 | Installation von Windows 10 | Schritt-für-Schritt Anleitung](https://www.youtube.com/watch?v=9Ehgzgg-X48&list=PLRcp6YbTf6Qk3pIZnrKBTEJ8lQl5NZujz)

In the Video the Guide uses a Windows 10-ISO. But the following guide works for Windows 10 and 11.

## Overview

This guide provides a step-by-step approach to installing Windows 11 on a Proxmox server. It covers the necessary preparations, installation steps, and post-installation configurations.

## Preparation Steps

### 1. Download Windows 11 ISO
- Visit the Microsoft website and download the Media Creation Tool to obtain the Windows 11 ISO file.
- This is essential for the installation process.

### 2. Download VirtIO Drivers
- Download the VirtIO drivers for Windows from the Proxmox website.
- These drivers are crucial for proper communication between the Windows VM and the Proxmox host.

### 3. Upload Files to Proxmox
- Log in to your Proxmox host and navigate to the local storage.
- Upload both the Windows 11 ISO and the VirtIO drivers.

## Installation Steps

### 4. Create a New Virtual Machine (VM)
- Right-click on your Proxmox host and select "Create VM."
- Assign an ID and name (e.g., vm-Windows 11).
- Select the Windows 11 ISO as the boot disk.

### 5. Configure VM Settings
- Set the desired number of cores (e.g., 4) and RAM (e.g., 6 GB).
- Add a second disk for the VirtIO drivers.

### 6. Start the VM
- Start the VM and connect via VNC.
- The Windows installer will load.

### 7. Install Windows
- Follow the prompts to install Windows.
- When asked for a disk, you may need to load the VirtIO drivers to see the disk.

### 8. Post-Installation Configuration
- After installation, install the VirtIO drivers to ensure all hardware functions correctly.
- This includes network and audio drivers.

## Final Steps

### 9. Remote Desktop Setup
- Set a password for the user account.
- Enable remote desktop connections.
- This allows access to the VM without needing VNC.

### 10. Resource Management
- Adjust the VM settings in Proxmox to ensure that the resource allocation reflects the actual usage.
- This helps in optimizing performance.

### 11. Cleanup
- Remove any unnecessary ISO files from the VM settings.
- This prevents confusion in future sessions.

## Important Notes

- **Backup**: Always ensure that you have backups of important data before making significant changes to your virtual machines.
- **Troubleshooting**: If you encounter issues with drivers, refer to the Proxmox documentation for troubleshooting tips.

## Conclusion

This guide should help you successfully install and configure Windows 11 on your Proxmox server while ensuring that all necessary steps are clear and easy to follow!