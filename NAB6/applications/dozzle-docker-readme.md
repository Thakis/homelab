# in progress

docker run -d --name dozzle-agent \
  --restart unless-stopped \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -p 7007:7007 \
  amir20/dozzle:latest agent


docker run -d --name dozzle-ui \
  --restart unless-stopped \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -p 8081:8080 \
  amir20/dozzle:latest \
  --remote-agent 192.168.178.200:7007 \
  --remote-agent 192.168.178.206:7007 \
  --remote-agent 192.168.178.209:7007 \
  --remote-agent 192.168.178.214:7007 \
  --remote-agent 192.168.178.215:7007 \
  --remote-agent 192.168.178.217:7007 \
  --remote-agent 192.168.178.218:7007 \
  --remote-agent 192.168.178.219:7007 \
  --remote-agent 192.168.178.221:7007 \
  --remote-agent 192.168.178.222:7007 \
  --remote-agent 192.168.178.223:7007 \
  --remote-agent 192.168.178.226:7007 \
  --remote-agent 192.168.178.228:7007 \
  --remote-agent 192.168.178.210:7007