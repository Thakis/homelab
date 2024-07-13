1. Terminalzugang über Task einrichten
- https://youtu.be/2X1vrnZBpzc?si=2cJ2BYThztjStY7B&t=387

2. install portainer

3. install portainer agent
# sudo docker run -d -p 9001:9001 --name portainer_agent --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /volume1/@docker/volumes:/var/lib/docker/volumes portainer/agent