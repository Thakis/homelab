# Baikal CalDAV/CardDAV Server Installation Guide

## Overview

[Baikal](https://sabre.io/baikal/) is a lightweight CalDAV and CardDAV server that provides easy synchronization for calendars and contacts. This guide explains how to install and configure Baikal using Docker.

## Quick Reference

- **Project Website**: [sabre.io/baikal](https://sabre.io/baikal/)
- **Docker Installation Guide**: [sabre.io/baikal/docker-install](https://sabre.io/baikal/docker-install/)
- **GitHub Repository**: [ckulka/baikal-docker](https://github.com/ckulka/baikal-docker)
- **Docker Hub**: [ckulka/baikal](https://hub.docker.com/r/ckulka/baikal/)

## Prerequisites

- Docker and Docker Compose installed
- Basic understanding of command line operations
- A server or NAS with direct internet access

## Installation Options

### Method 1: Using Docker Run

```bash
# Create a directory for persistent storage
mkdir -p /path/to/baikal/config
mkdir -p /path/to/baikal/data

# Run the Baikal container
docker run -d \
  --name baikal \
  -p 80:80 \
  -v /path/to/baikal/config:/var/www/baikal/config \
  -v /path/to/baikal/data:/var/www/baikal/Specific \
  ckulka/baikal:latest
```

### Method 2: Using Docker Compose (Recommended)

1. Create a `docker-compose.yml` file:

```yaml
version: '3'

services:
  baikal:
    image: ckulka/baikal:latest
    restart: unless-stopped
    ports:
      - "80:80"
    volumes:
      - ./config:/var/www/baikal/config
      - ./data:/var/www/baikal/Specific
```

2. Start the container:

```bash
docker-compose up -d
```

## Initial Configuration

1. After starting the container, open your web browser and navigate to:
   ```
   http://your-server-ip/admin
   ```

2. Follow the setup wizard:
   - Create your admin account
   - Configure the database (SQLite is used by default)
   - Set up time zone settings

3. Once the setup is complete, you can:
   - Create users
   - Set up calendar and contact collections
   - Configure access rights

## Using with CalDAV/CardDAV Clients

### Connection URLs

For CalDAV (Calendars):
```
http://your-server-ip/dav/{username}/calendars/
```

For CardDAV (Contacts):
```
http://your-server-ip/dav/{username}/addressbooks/
```

### Client Setup Examples

#### iOS/macOS

1. Go to Settings > Calendar > Accounts > Add Account > Other
2. Select "Add CalDAV Account" or "Add CardDAV Account"
3. Enter:
   - Server: your-server-ip
   - Username: your-baikal-username
   - Password: your-baikal-password

#### Thunderbird

1. Install the TbSync and Provider for CalDAV & CardDAV add-ons
2. Add a new CalDAV & CardDAV account
3. Enter the connection URLs as specified above

## Security Recommendations

### Enable HTTPS

For production environments, it's strongly recommended to set up HTTPS. You can use a reverse proxy like Nginx or Traefik with Let's Encrypt.

Example Nginx configuration:

```nginx
server {
    listen 443 ssl;
    server_name calendar.example.com;

    ssl_certificate /etc/letsencrypt/live/calendar.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/calendar.example.com/privkey.pem;

    location / {
        proxy_pass http://localhost:80;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

### Using Docker with HTTPS

For direct HTTPS configuration with Docker, use the Apache-SSL image:

```yaml
version: '3'

services:
  baikal:
    image: ckulka/baikal:apache-ssl
    restart: unless-stopped
    ports:
      - "443:443"
    volumes:
      - ./config:/var/www/baikal/config
      - ./data:/var/www/baikal/Specific
      - ./ssl/cert.pem:/etc/ssl/certs/ssl-cert-snakeoil.pem
      - ./ssl/cert.key:/etc/ssl/private/ssl-cert-snakeoil.key
```

## Backup

To backup your Baikal installation, simply copy the contents of your mapped volumes:

```bash
# Create a backup
tar -czf baikal-backup.tar.gz /path/to/baikal/config /path/to/baikal/data
```

To restore:

```bash
# Restore from backup
tar -xzf baikal-backup.tar.gz -C /
```

## Upgrading

To upgrade Baikal to a newer version:

```bash
# Pull the latest image
docker pull ckulka/baikal:latest

# Restart your container
docker-compose down
docker-compose up -d
```

## Troubleshooting

### Common Issues

1. **Permission Problems**: Ensure the Docker container has the correct permissions for the mounted volumes:
   ```bash
   sudo chown -R www-data:www-data /path/to/baikal/config
   sudo chown -R www-data:www-data /path/to/baikal/data
   ```

2. **Connection Issues**: Check that your firewall allows connections to the ports you've configured.

3. **Database Errors**: If you encounter database errors, check the logs:
   ```bash
   docker logs baikal
   ```

### Accessing Logs

```bash
# View container logs
docker logs -f baikal
```

## Advanced Configuration

### Using MySQL/MariaDB Instead of SQLite

1. Set up a MySQL/MariaDB container:

```yaml
version: '3'

services:
  baikal:
    image: ckulka/baikal:latest
    restart: unless-stopped
    ports:
      - "80:80"
    volumes:
      - ./config:/var/www/baikal/config
      - ./data:/var/www/baikal/Specific
    depends_on:
      - db

  db:
    image: mariadb:10.5
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: rootpwd
      MYSQL_DATABASE: baikal
      MYSQL_USER: baikal
      MYSQL_PASSWORD: baikaldbpass
    volumes:
      - ./mysql:/var/lib/mysql
```

2. During initial Baikal setup, choose MySQL and enter the database details.

## Additional Resources

- [Baikal Documentation](https://sabre.io/baikal/documentation/)
- [SabreDAV Documentation](https://sabre.io/dav/)
- [Docker Documentation](https://docs.docker.com/)

## Community Support

- [GitHub Issues](https://github.com/sabre-io/Baikal/issues)
- [Sabre.io Forum](https://groups.google.com/g/sabredav-discuss)

---

This guide was compiled based on the official Baikal Docker installation documentation and community best practices. For the most up-to-date information, please refer to the [official documentation](https://sabre.io/baikal/).