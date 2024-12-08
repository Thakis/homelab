# Docker and Portainer Setup Guide

## Prerequisites
- Docker installed
- Terminal access

## Setup Steps

### 1. Terminal Access Configuration
- Watch detailed guide: [Terminal Access Setup](https://youtu.be/2X1vrnZBpzc?si=2cJ2BYThztjStY7B&t=387)

### 2. Install Portainer

#### Portainer Agent Installation
Run the following Docker command to install the Portainer agent:

```bash
sudo docker run -d \
  -p 9001:9001 \
  --name portainer_agent \
  --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /volume1/@docker/volumes:/var/lib/docker/volumes \
  portainer/agent
```

## Notes
- Ensure you have sudo privileges
- Verify Docker is running before installation
- Adjust volume paths if necessary for your specific setup