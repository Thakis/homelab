# Install Watchtower
```bash
docker run -it -d \
  --name watchtower \
 --restart unless-stopped \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -e WATCHTOWER_NOTIFICATIONS=gotify \
  -e WATCHTOWER_NOTIFICATION_GOTIFY_URL="http://192.168.178.25:8050" \
  -e WATCHTOWER_NOTIFICATION_GOTIFY_TOKEN="TOKEN" \
  containrrr/watchtower:latest \
  --cleanup \
  --include-restarting \
  --rolling-restart \
  --include-stopped \
  --schedule "0 0 2 * *"