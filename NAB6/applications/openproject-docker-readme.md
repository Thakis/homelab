# OpenProject - Docker Compose Installation Guide

This guide covers the essential steps to install and run OpenProject using Docker Compose. The installation is based on the official documentation: [https://www.openproject.org/docs/installation-and-operations/installation/docker-compose/](https://www.openproject.org/docs/installation-and-operations/installation/docker-compose/)

## 1. Prerequisites

Ensure the following are installed:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [Git](https://git-scm.com/downloads)

Recommended system resources: at least 4 GB RAM and 2 CPU cores.

## 2. Directory Structure

Clone the official OpenProject deployment repository:

```bash
mkdir -p ~/openproject
cd ~/openproject
git clone https://github.com/opf/openproject-docker-compose.git --depth=1 --branch=stable/17 openproject
cd compose
```

> The branch version (`stable/17`) should match the currently recommended version in the official documentation.

## 3. Create Environment File

Copy the example configuration and adjust it:

```bash
cp .env.example .env
nano .env
```

Important variables in the `.env` file:

```env
# Port on which OpenProject will be available
PORT=8080

# Hostname or IP address (without http://)
OPENPROJECT_HOST__NAME=192.168.178.215:8080

# Disable HTTPS if no reverse proxy with TLS is used
OPENPROJECT_HTTPS=false

# Database password (make sure to change it!)
POSTGRES_PASSWORD=a_secure_password

# Docker image tag
TAG=17-slim
```

> Note: If OpenProject is run without HTTPS, `OPENPROJECT_HTTPS=false` must be set, otherwise login will not work.

## 4. Persistent Data (optional)

By default, Docker creates volumes for the database and files. To use fixed directories instead, adjust the `.env` file:

```bash
mkdir -p /opt/openproject/pgdata /opt/openproject/assets
```

```env
OPDATA=/opt/openproject/assets
PGDATA=/opt/openproject/pgdata
```

## 5. Start the Containers

From the `~/openproject/compose` directory:

```bash
docker compose pull
docker compose up -d
```

The first start may take a few minutes. Check the status:

```bash
docker compose ps
docker compose logs -f proxy
```

## 6. First Login

Open the interface in your browser: [http://localhost:8080](http://localhost:8080)

Default credentials:

| Username | Password |
|----------|----------|
| `admin`  | `admin`  |

> The password must be changed on first login.

## 7. Updating

To update OpenProject:

```bash
cd ~/openproject/compose
git pull origin stable/17
docker compose pull
docker compose up -d
```

## 8. Backup (recommended)

Back up the database and files before every update:

```bash
docker compose exec db pg_dumpall -U postgres > openproject_backup.sql
tar -czf openproject_assets.tar.gz /opt/openproject/assets
```

## 9. Stopping and Removing

```bash
# Stop
docker compose down

# Stop and delete volumes (warning: data loss!)
docker compose down -v
```

---

For further customization and advanced configuration (e.g. reverse proxy, SSL, SMTP), refer to the official documentation:
👉 [https://www.openproject.org/docs/installation-and-operations/installation/docker-compose/](https://www.openproject.org/docs/installation-and-operations/installation/docker-compose/)
