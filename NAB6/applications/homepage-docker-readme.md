# Homepage - Docker Installation Guide

This guide covers the essential steps to install and run Homepage using Docker.

## 1. Prerequisites

Ensure the following are installed:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## 2. Directory Structure

Create a directory for Homepage configuration:

```bash
mkdir -p ~/homepage
cd ~/homepage
````

## 3. Create Docker Compose File

Create a `docker-compose.yml` file in the `~/homepage` directory:

```yaml
version: "3.8"

services:
  homepage:
    image: ghcr.io/gethomepage/homepage:latest
    container_name: homepage
    volumes:
      - /root/homepage/config:/app/config
      - /root/homepage/images:/app/public/images
      - /root/homepage/icons:/app/public/icons
    ports:
      - 3000:3000
    environment:
      HOMEPAGE_ALLOWED_HOSTS: gethomepage.dev,192.168.178.215:3000 # required, may need port. See gethomepage.dev/installation/#homepage_allowed_hosts
      PUID: $PUID
      PGID: $PGID
    restart: unless-stopped
```

## 4. Create Configuration Directory and Files

Inside the `~/homepage/config` folder, create minimal required config files:

```bash
mkdir config
cd config
touch settings.yaml services.yaml widgets.yaml bookmarks.yaml
```

> These files can be edited later to customize Homepage.

## 5. Start the Container

From the `~/homepage` directory:

```bash
docker-compose up -d
```

Visit the interface at: [http://localhost:3000](http://localhost:3000)

## 6. Updating

To update Homepage:

```bash
docker-compose pull
docker-compose up -d
```

---

For full customization and advanced usage, refer to the official documentation:
👉 [https://gethomepage.dev/installation/docker/](https://gethomepage.dev/installation/docker/)