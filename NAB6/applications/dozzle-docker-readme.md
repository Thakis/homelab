# in progress

Run the Dozzle agent on every Docker host you want to monitor:

```bash
docker run -d --name dozzle-agent \
  --restart unless-stopped \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -p 7007:7007 \
  amir20/dozzle:latest agent
```

Run the Dozzle UI on one host and add one `--remote-agent` line per agent
(replace the `<HOST_n_IP>` placeholders with the IP addresses of your Docker hosts):

```bash
docker run -d --name dozzle-ui \
  --restart unless-stopped \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -p 8081:8080 \
  amir20/dozzle:latest \
  --remote-agent <HOST_1_IP>:7007 \
  --remote-agent <HOST_2_IP>:7007 \
  --remote-agent <HOST_3_IP>:7007
```
