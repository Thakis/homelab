# Install Gotify
```bash
docker run -p 8050:80 -e TZ="Europe/Berlin" -v /var/gotify/data:/app/data ghcr.io/gotify/server-arm64
```
Official documentation: [Gotify Install Guide](https://gotify.net/docs/install)