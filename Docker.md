# Useful docker commands
To start a docker via Docker Compose use: 
`sudo docker compose up`
To log in to the shell for a specific container use: 
`docker exec -it <mycontainer> bash`

# Docker post install tasks
Source: https://docs.docker.com/engine/install/linux-postinstall/
Add a specific user to the Docker group for Docker command execution without sudo like follows.
First create the docker group if not already automatically added during install:
`sudo groupadd docker`
Now add the target user to the docker group:
`sudo usermod -aG docker $USER`

Source: https://docs.docker.com/config/containers/logging/syslog/
Set up a syslog to get Docker logs by adding a file called `daemon.json` in the folder `/etc/docker/` and add a configuration like this:
```
{
  "log-driver": "syslog",
  "log-opts": {
    "syslog-address": "udp://1.2.3.4:1111"
  }
}
```

# Docker Portainer Agent
A Portainer Agent can be used to interact with a Docker environment on a different server. If Portainer is set up on a central server it can be used to connect to the agent and act as an interface without needing to log into the remote server. This way only one master Partainer CE container has to be run.
To install Portainer Agent on remote servers the following Docker Compose file can be used:
```
version: "3"
services:
  agent:
    container_name: portainer_agent
    image: portainer/agent
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /var/lib/docker/volumes:/var/lib/docker/volumes
    ports:
      - "9001:9001"
```
To connect the remote Agent to the primary server the Agent has to be added as Agent through the Environments Settings page in Portainer CE.