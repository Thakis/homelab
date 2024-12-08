# Paperless-NGX Docker Setup Guide

## Video Tutorial
[Watch Installation Tutorial](https://www.youtube.com/watch?v=2odgHEaIFFI&list=PL3-bM7Aq1pUoyqlHZyfBU9pMeBBUTK8UI&index=4)

## Project Repository
[GitHub Repository](https://github.com/RPiList/SynVideos/tree/main/Videos/DockerPaperlessNGX)

## Overview

This guide provides a step-by-step walkthrough for setting up Paperless-NGX using Docker, with a specific focus on integration with an Epson Scanner's consume folder.

## Prerequisites

- Docker
- Docker Compose
- Epson Scanner
- Synology NAS (recommended)

## Folder Structure

```
/docker/paperless-ngx/
│
├── docker-compose.yml
├── data/
│   ├── consume/       # Epson Scanner input folder
│   ├── export/        # Document export location
│   ├── media/         # Media files
│   └── postgres/      # PostgreSQL database files
│
└── .env              # Environment configuration
```

## Configuration Steps

### 1. Prepare Docker Compose File

Create a `docker-compose.yml` file with the following configuration:

```yaml
version: '3.8'
services:
  broker:
    image: docker.io/library/redis:7
    restart: unless-stopped
    volumes:
      - redis_data:/data

  webserver:
    image: ghcr.io/paperless-ngx/paperless-ngx:latest
    restart: unless-stopped
    depends_on:
      - broker
      - db
    ports:
      - 8000:8000
    volumes:
      - ./data/consume:/usr/src/paperless/consume
      - ./data/export:/usr/src/paperless/export
      - ./data/media:/usr/src/paperless/media
      - ./data/data:/usr/src/paperless/data
    environment:
      - PAPERLESS_REDIS_URL=redis://broker:6379
      - PAPERLESS_DBENGINE=postgresql
      - PAPERLESS_DBHOST=db
      - PAPERLESS_DBUSER=${DB_USER}
      - PAPERLESS_DBPASS=${DB_PASS}
      - PAPERLESS_DBNAME=${DB_NAME}

  db:
    image: docker.io/library/postgres:15
    restart: unless-stopped
    volumes:
      - ./data/postgres:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=${DB_USER}
      - POSTGRES_PASSWORD=${DB_PASS}
      - POSTGRES_DB=${DB_NAME}

volumes:
  redis_data:
```

### 2. Create .env File

Create a `.env` file with the following variables:

```
DB_USER=paperless
DB_PASS=your_secure_password
DB_NAME=paperless
```

### 3. Epson Scanner Configuration

- Configure your Epson Scanner to save scanned documents to `/docker/paperless-ngx/data/consume`
- Ensure the scanner saves files in supported formats (PDF, JPG, PNG)

### 4. Start Paperless-NGX

```bash
docker-compose up -d
```

### 5. Initial Setup

- Access the web interface at `http://your-nas-ip:8000`
- Create an initial admin user
- Configure document consumption settings

## Recommended Settings

- Enable automatic document matching
- Set up OCR language support
- Configure document tags and correspondents

## Maintenance

- Regularly backup your Docker volumes
- Monitor disk space
- Update containers periodically

## Troubleshooting

- Check container logs: `docker-compose logs`
- Verify consume folder permissions
- Ensure network connectivity

## Security Considerations

- Use strong passwords
- Limit port exposure
- Keep Docker and images updated

## Resources

- [Paperless-NGX Documentation](https://docs.paperless-ngx.com/)
- [Docker Documentation](https://docs.docker.com/)

## License

This setup follows the licensing terms of Paperless-NGX and Docker.