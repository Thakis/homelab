
# CrowdSec Installation Guide

## Video Resources
- [CROWDSEC - Step for Step installation guide](https://www.youtube.com/watch?v=hpxW4zDBoTI)
- [Install and Configure CrowdSec on Proxmox VE 8 – How-to](https://schroederdennis.de/tutorial-howto/crowdsec-auf-proxmox-ve-8-installieren-und-einrichten-howto/)

## Installation Steps

### 1. Add the CrowdSec Repository
The first step is to add the CrowdSec repository:
```bash
curl -s https://packagecloud.io/install/repositories/crowdsec/crowdsec/script.deb.sh | sudo bash
```

### 2. Install CrowdSec
Install CrowdSec on your system:
```bash
sudo apt install crowdsec
```

### 3. Add the Firewall IPTables Bouncer
The bouncer is responsible for keeping the IPTables lists up to date:
```bash
sudo apt install crowdsec-firewall-bouncer
```

### 4. Modify Configuration for SQLite Database
Add the `use_wal: true` setting in the `db_config` section. Edit the file:
```bash
nano /etc/crowdsec/config.yaml
```
Update the `db_config` section as follows:
```yaml
db_config:
  log_level: info
  type: sqlite
  db_path: /var/lib/crowdsec/data/crowdsec.db
  use_wal: true
```

### 5. Start CrowdSec
Start the software with the following command (auto-start is enabled by default):
```bash
service crowdsec start
```

### 6. Optional: CrowdSec Dashboard
To integrate the agent with the CrowdSec dashboard:
1. Log in to the CrowdSec website and create a new engine.
2. Obtain the enrollment code.
3. Run the following command with your API key:
```bash
sudo cscli console enroll #useoneapikey
```

### 7. Optional: Local CrowdSec Dashboard
To set up a local CrowdSec dashboard, run:
```bash
cscli dashboard setup --listen 0.0.0.0
```