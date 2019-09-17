
# Docker

## Docker Easy Installation

```shell
curl -sSL https://get.docker.com | sudo sh
```

## Tipps and Tricks

```shell
# Show log output
docker logs <container>

# Connect to a running container
docker exec -it <container> bash

# Stop all containers
docker stop $(docker ps -aq)

# Delete all containers
docker rm $(docker ps -aq)

# Delete all images
docker rmi -f $(docker images -q)
```