# Proxmox Backup Server Installation on Synology NAS

[Watch Tutorial Video](https://www.youtube.com/watch?v=abf2D9ikkn8&list=PLRcp6YbTf6Qk3pIZnrKBTEJ8lQl5NZujz&index=6)

## Proxmox Backup Server Installation and Configuration on Synology NAS

This guide details installing and configuring a Proxmox Backup Server (PBS) on a Synology NAS. It emphasizes incremental backups and deduplication for efficient storage and network usage.

## 1. Preparation

- Download the Proxmox Backup Server 3.1 ISO image
- It's recommended to run PBS on a separate device for redundancy. A Synology NAS is used in this example

## 2. Synology NAS Setup

- Create a virtual machine (VM) in the Synology Virtual Machine Manager. Allocate at least 2GB RAM
- Create two virtual hard disks:
  - One smaller for the OS (e.g., 20GB)
  - A larger one for backups (e.g., 500GB)
- Create a network for the Backup Server
- Upload the downloaded PBS ISO image

## 3. Proxmox Backup Server Installation

- Start the VM and boot from the ISO
- Follow the graphical installer
- Choose the storage location for the OS (the smaller disk)
- Set a password and configure network settings (IP address, gateway)
  - Remember to reserve the IP address on your DHCP server
- Install the PBS

## 4. Post-Installation Configuration

- Access the PBS web interface using the assigned IP address and the credentials you set during installation
- Format the larger disk using GPT and initialize it
- Create a directory (e.g., using ext4) as a datastore for backups
- Add the datastore to the Proxmox hypervisor

## 5. Backup Job Creation

- Create a backup job in the Proxmox hypervisor, specifying:
  - VMs to back up
  - Schedule
  - Datastore

## 6. Backup Retention Policy

- Configure a retention policy using the prune options to manage storage space
- Use the [PBS Prune Simulator](https://proxmox.com/doc/prune-simulator) to visualize retention settings

## 7. Verification and Restore

- Enable backup verification (`verify always`) for data integrity
- Restore backups as needed. Live restore is possible

## Advantages of Proxmox Backup Server

- Incremental backups reduce network load and storage space
- Deduplication further optimizes storage usage