# Proxmox Backup Server Installation on Synology NAS

This guide summarizes the YouTube video **"Proxmox Backup Server Installation on Synology NAS"**, which provides a detailed walkthrough for setting up Proxmox Backup Server (PBS) on a Synology NAS. It is aimed at users who want to enhance their backup infrastructure by integrating PBS into their existing Synology environment.

---

## 🧰 Requirements

- Synology NAS with Virtual Machine Manager (VMM) or Docker support
- Proxmox Backup Server ISO or container image
- Basic knowledge of SSH and the Synology DSM interface

---

## 🛠️ Installation Steps

### 1. Preparing the Synology NAS

- Enable Virtual Machine Manager (VMM) or Docker on the NAS
- Download the Proxmox Backup Server ISO image from the official website

### 2. Creating and Configuring the Virtual Machine

- Create a new VM in VMM with the following specs:
  - Assign appropriate CPU, RAM, and storage
  - Attach the PBS ISO image as the boot medium
- Start the VM and follow the PBS installation instructions

### 3. Network and Storage Integration

- Assign a static IP to the VM for stable network access
- Mount additional storage directories or external drives as PBS datastores

---

## 🔄 Backup Synchronization Setup

- Configure pull sync jobs in PBS to sync backups from other PBS instances or storage locations
- Set up remote connections using hostname, port, and authentication credentials
- Schedule regular sync intervals to maintain updated backups

---

## 🧹 Maintenance and Automation

- Create prune jobs to automatically remove old backups based on retention policies
- Set up garbage collection (GC) jobs to free unused data and optimize storage
- Schedule regular backup jobs for connected Proxmox VE instances

---

## ✅ Benefits of This Setup

- **Cost-Effective**: Uses existing Synology NAS hardware
- **Centralized Management**: Unified backup strategy for various systems
- **Flexible**: Supports integration of additional storage and PBS instances
- **Secure**: Regular backups and syncs reduce risk of data loss

---

## 🔗 Additional Resources

- [Proxmox Backup Server Documentation](https://pbs.proxmox.com/docs/)
- [Synology Virtual Machine Manager Guide](https://www.synology.com/en-global/knowledgebase/DSM/help/VirtualMachineManager)
- [Proxmox Forum Discussion on PBS & USB Drive Sync](https://forum.proxmox.com/threads/proxmox-pbs-lxc-mit-usb-festplatte-für-backup-synchronisation-einrichten.159155/)

---

This setup provides an efficient and secure backup solution for IT infrastructures leveraging a Synology NAS and Proxmox Backup Server.