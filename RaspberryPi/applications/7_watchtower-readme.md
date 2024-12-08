# Install Watchtower
```bash
docker run -it -d \
  --name watchtower \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -e WATCHTOWER_NOTIFICATIONS=gotify \
  -e WATCHTOWER_NOTIFICATION_GOTIFY_URL="http://192.168.178.25:8050" \
  -e WATCHTOWER_NOTIFICATION_GOTIFY_TOKEN="AWP-4e29yKkHzz4" \
  containrrr/watchtower:latest \
  --cleanup \
  --include-restarting \
  --rolling-restart \
  --include-stopped \
  --schedule "0 0 2 * **"
```