# Apache Guacamole Docker Setup Guide

This guide explains how to deploy **Apache Guacamole** using the `jwetzell/guacamole` Docker image (version `1.5.5`) with a built-in PostgreSQL database and TOTP (Time-based One-Time Password) extension enabled.

## Features

- Guacamole 1.5.5
- Built-in PostgreSQL database
- TOTP (2FA) support
- Config persistence via Docker volumes
- Accessible on port 8080

## Prerequisites

- A system with Docker and Docker Compose installed
- Internet access to pull Docker images
- Basic understanding of Docker

## 1. Create a `docker-compose.yml` File

Create a directory for your project and inside that directory, create a file named `docker-compose.yml` with the following content:

```yaml
version: "3.8"

services:
  guacamole:
    image: jwetzell/guacamole:1.5.5
    container_name: guacamole
    restart: unless-stopped
    volumes:
      - postgres:/config
    ports:
      - 8080:8080
    environment:
      TZ: Europe/Berlin
      EXTENSIONS: "auth-totp"

volumes:
  postgres:
    driver: local
```

## 2. Start the Container

Run the following command in the same directory as your `docker-compose.yml` file:

```bash
docker compose up -d
```

This will:
- Pull the `jwetzell/guacamole:1.5.5` image if not already available
- Start the Guacamole container
- Expose the web interface on [http://localhost:8080](http://localhost:8080)

## 3. Initial Access

Open a web browser and go to:

```
http://localhost:8080
```

### Default Credentials

- **Username:** `guacadmin`
- **Password:** `guacadmin`

> ⚠️ **Important**: For security, change the default password immediately after logging in.

## 4. Notes

- Configuration is stored in the `postgres` volume.
- TOTP two-factor authentication is enabled by default via the `auth-totp` extension.
- The container's timezone is set to `Europe/Berlin`.

## 5. Stopping and Removing

To stop the container:

```bash
docker compose down
```

To stop and remove volumes (including configuration data):

```bash
docker compose down -v
```

## 6. Backup and Restore

To back up the configuration:

```bash
docker run --rm -v guacamole_postgres:/config -v $(pwd):/backup busybox tar czf /backup/guac-config-backup.tar.gz /config
```

To restore:

```bash
docker run --rm -v guacamole_postgres:/config -v $(pwd):/backup busybox sh -c "rm -rf /config/* && tar xzf /backup/guac-config-backup.tar.gz -C /"
```

---

**Author:** [Michael]  
**Last updated:** 2025-05-23  
**Reference:** [jwetzell/docker-guacamole](https://github.com/jwetzell/docker-guacamole)
