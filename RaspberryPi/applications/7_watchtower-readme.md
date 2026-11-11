# Install Watchtower
```bash
docker run -it -d \
  --name watchtower \
 --restart unless-stopped \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -e WATCHTOWER_NOTIFICATIONS_HOSTNAME= \
  -e WATCHTOWER_NOTIFICATION_URL="http://192.168.178.25:8050" \
 gotify://gotify.michaelgoehringer.de/MY_OWN_TOKENG --cleanup \
  --include-restarting \
  --rolling-restart \
  --include-stopped \
  --schedule "0 0 2 * *"