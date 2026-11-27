# Install Watchtower

Replace the placeholders in `<...>` with your own values before running the command.
Notifications are sent via Gotify (Shoutrrr URL). Keep the token secret and never commit it.

```bash
docker run -it -d \
  --name watchtower \
  --restart unless-stopped \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -e WATCHTOWER_NOTIFICATIONS_HOSTNAME="<HOSTNAME>" \
  -e WATCHTOWER_NOTIFICATION_URL="gotify://<GOTIFY_HOST>:<GOTIFY_PORT>/<GOTIFY_TOKEN>?disableTLS=yes" \
  containrrr/watchtower:latest \
  --cleanup \
  --include-restarting \
  --rolling-restart \
  --include-stopped \
  --schedule "0 0 2 * * *"
```

Notes:
- `disableTLS=yes` is only needed if Gotify is reachable via plain HTTP inside your network. Remove it if you use HTTPS.
- `--schedule` uses a cron expression with **six** fields (seconds first). The example runs every day at 02:00.
