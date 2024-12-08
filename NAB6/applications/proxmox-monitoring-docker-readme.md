# Proxmox Monitoring Setup Guide

## Links
- [Proxmox Monitoring Tutorial Video](https://www.youtube.com/watch?v=cO5FpCOPbwM)
- [Detailed Commands Document](https://docs.google.com/document/d/14qaRI_Z9TQvOr-TA5vtpYjnibZjiD-sbTp7uNyE0KhM/edit) by [CS Obsession](https://www.youtube.com/@csobsession)

## InfluxDB Setup

### Installation Steps
```bash
# Update system packages
apt update && apt upgrade

# Add InfluxDB repository key
wget -q https://repos.influxdata.com/influxdata-archive_compat.key
echo 'deb [signed-by=/etc/apt/trusted.gpg.d/influxdata-archive_compat.gpg] https://repos.influxdata.com/debian stable main' | tee /etc/apt/sources.list.d/influxdata.list
cat influxdata-archive_compat.key | gpg --dearmor | tee /etc/apt/trusted.gpg.d/influxdata-archive_compat.gpg > /dev/null

# Install InfluxDB
apt update && apt install influxdb2

# Start and check InfluxDB service
service influxdb start
service influxdb status

# Initial setup
influx setup
```

## Grafana Setup

### Installation Steps
```bash
# Add Grafana repository key
wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | tee -a /etc/apt/sources.list.d/grafana.list

# Install Grafana
apt update
apt install grafana

# Configure and start Grafana service
systemctl daemon-reload
systemctl start grafana-server
systemctl status grafana-server
systemctl enable grafana-server.service
```

## Access Information

### InfluxDB
- **Port**: 8086

### Grafana
- **Port**: 3000
- **Community Dashboard ID**: 17051

## Notes
- Ensure you have the necessary permissions when running these commands
- It's recommended to run these commands with `sudo` or as root
- Always backup your configuration before making changes