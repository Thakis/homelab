```markdown
# Setting Up Remote Hyper Backup Without Cloud Services

[![Watch the Tutorial](https://img.youtube.com/vi/D8lJcf0V_-4/0.jpg)](https://www.youtube.com/watch?v=D8lJcf0V_-4)  
[Watch the video tutorial here](https://www.youtube.com/watch?v=D8lJcf0V_-4)

---

## Overview
This guide details the process of setting up a remote backup using Synology's **Hyper Backup** without relying on cloud services. The backup will be transferred to a remote Synology NAS located off-site.

---

## Prerequisites
1. **Synology NAS Devices**: 
   - One at the source location and one at the destination (e.g., a relative's house).
2. **Network Connection**: 
   - Ensure both NAS devices are connected to a network with sufficient bandwidth (e.g., symmetrical fiber optic).
3. **Software Installation**:  
   - Install **Hyper Backup Vault** on the destination NAS for receiving backups.  
   - Install **Tailscale** for secure VPN connectivity, allowing devices to connect without opening router ports.  

---

## Setup Steps

### 1. Initial Backup on Local Network
- Run the initial backup locally to transfer large volumes of data quickly.  
- After the initial backup, switch to incremental backups over the internet.

### 2. Tailscale Configuration
- Set up **Tailscale** on both NAS devices to create a secure connection.  
- Ensure outbound connections are enabled for Tailscale on **DSM-7 or above**.

### 3. Create Backup Folder
- On the destination NAS, create a shared folder named **"backups"** for storing the incoming backup data.

### 4. User Management
- Create a dedicated user for the backup function on the remote NAS.  
- Grant this user **read/write access** only to the "backups" folder.

### 5. Setting Up Hyper Backup on Source NAS
- Install **Hyper Backup** on the source NAS and configure it to back up to the remote NAS.  
- Use either the local IP or Tailscale IP for the connection.  
- Log in using the backup user credentials created earlier.

### 6. Backup Task Configuration
- Select folders to back up and configure settings, such as:  
  - Task notifications  
  - Compression  
  - Scheduling  
  - Client-side encryption for security  
- Set the backup rotation to manage file versions efficiently.

---

## Incremental Backups
- After the initial backup, switch to using the **Tailscale IP** for subsequent backups.  
- This allows for transferring only changed data, reducing backup time and bandwidth usage.  
- Verify successful backups by checking the destination NAS.

---

## Conclusion
Setting up a remote Hyper Backup with Synology enables full control over your data without relying on cloud services.  
This method is efficient, secure, and cost-effective, providing peace of mind for your data protection needs.
```