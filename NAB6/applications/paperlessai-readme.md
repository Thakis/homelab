# Paperless-AI Installation Guide

## Overview
Paperless-AI is a document management application with AI capabilities. This guide describes various installation methods.

## Prerequisites
- Docker and Docker Compose installed
- Git installed (for Method 1)
- At least 2GB of free disk space
- Port 3000 available

## Installation

### Method 1: Using Docker Compose (Recommended)

1. **Clone the repository**
   ```bash
   git clone https://github.com/clusterzx/paperless-ai.git
   ```

2. **Navigate to the project directory**
   ```bash
   cd paperless-ai
   ```

3. **Start the containers**
   ```bash
   docker-compose up -d
   ```

### Method 2: Single Docker Container

Alternatively, you can run Paperless-AI with a single Docker command:

```bash
docker run -d \
  --name paperless-ai \
  --network bridge \
  -v paperless-ai_data:/app/data \
  -p 3000:3000 \
  --restart unless-stopped \
  clusterzx/paperless-ai
```

### Method 3: Installation with Portainer

For installation via Portainer, you can use the Docker Compose file as a stack. An example video is available in the official documentation.

## Accessing the Application

After successful installation, Paperless-AI is accessible at:

```
http://localhost:3000
```

## Parameter Explanation

- `--name paperless-ai`: Name of the Docker container
- `--network bridge`: Use the default bridge network
- `-v paperless-ai_data:/app/data`: Persistent data storage
- `-p 3000:3000`: Port forwarding (Host:Container)
- `--restart unless-stopped`: Automatic container restart

## Data Volumes

The application uses a Docker volume (`paperless-ai_data`) for persistent data storage. This ensures that your documents and configurations are preserved even after container restarts.

## Troubleshooting

### Container won't start
- Check if port 3000 is already in use
- Ensure Docker is running
- Check Docker logs: `docker logs paperless-ai`

### Access issues
- Check firewall settings
- Ensure port 3000 is not blocked
- Try accessing via `http://127.0.0.1:3000`

## Uninstallation

### Docker Compose version
```bash
cd paperless-ai
docker-compose down -v
```

### Single container
```bash
docker stop paperless-ai
docker rm paperless-ai
docker volume rm paperless-ai_data
```

## Additional Resources

- GitHub Repository: https://github.com/clusterzx/paperless-ai
- Official Documentation: https://github.com/clusterzx/paperless-ai/wiki
- Installation videos are available in the official documentation

## Support

For questions or issues, visit the GitHub repository or create an issue.
