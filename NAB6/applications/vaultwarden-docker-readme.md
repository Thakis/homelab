# Vaultwarden Installation Guide

## Source
- [Vaultwarden GitHub Repository](https://github.com/AndresHardware/Vaultwarden)

## Preparation

### System Update and Prerequisites
```bash
# Update system packages
apt-get update && apt-get upgrade -y && apt autoremove -y

# Install required dependencies
apt install curl
apt install argon2

# Install Docker
curl -sSL https://get.docker.com | sh
apt install docker-compose -y
```

## Docker Installation Methods

### Method 1: Pull and Run Docker Image
```bash
# Pull the latest Vaultwarden image
docker pull vaultwarden/server:latest

# Run Vaultwarden container
docker run -d --name vaultwarden -v /vw-data/:/data/ -p 80:80 vaultwarden/server:latest
```

## Additional Recommendations

- Ensure you have sufficient disk space for `/vw-data/` volume
- Consider using a reverse proxy for added security
- Configure HTTPS for secure access
- Regularly update the Vaultwarden image

## Notes
- These instructions are for Debian/Ubuntu-based systems
- Root or sudo privileges are required for installation
- Always review and understand commands before executing