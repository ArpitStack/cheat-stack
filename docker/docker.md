# Docker CheatSheet

A comprehensive guide covering essential Docker commands and configurations for containerization and orchestration.

## Table of Contents

- [Installation & Setup](#installation--setup)
- [Docker Images](#docker-images)
- [Docker Containers](#docker-containers)
- [Docker Volumes](#docker-volumes)
- [Docker Networks](#docker-networks)
- [Docker Compose](#docker-compose)
- [Dockerfile](#dockerfile)
- [Docker Logs & Monitoring](#docker-logs--monitoring)
- [Docker Registry](#docker-registry)
- [Docker Swarm](#docker-swarm)

## Installation & Setup

Install Docker:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

Verify installation:

```bash
docker --version
```

Start Docker service:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

Check Docker system info:

```bash
docker info
```

## Docker Images

List available images:

```bash
docker images
```

Pull an image from Docker Hub:

```bash
docker pull <image-name>
```

Remove an image:

```bash
docker rmi <image-id>
```

Build an image from a Dockerfile:

```bash
docker build -t <image-name> .
```

## Docker Containers

Run a container:

```bash
docker run -d --name <container-name> <image-name>
```

List running containers:

```bash
docker ps
```

List all containers (including stopped ones):

```bash
docker ps -a
```

Stop a running container:

```bash
docker stop <container-id>
```

Start a stopped container:

```bash
docker start <container-id>
```

Remove a container:

```bash
docker rm <container-id>
```

Execute a command inside a running container:

```bash
docker exec -it <container-id> /bin/bash
```

## Docker Volumes

List volumes:

```bash
docker volume ls
```

Create a volume:

```bash
docker volume create <volume-name>
```

Attach a volume to a container:

```bash
docker run -d -v <volume-name>:/data <image-name>
```

Remove a volume:

```bash
docker volume rm <volume-name>
```

## Docker Networks

List networks:

```bash
docker network ls
```

Create a network:

```bash
docker network create <network-name>
```

Connect a container to a network:

```bash
docker network connect <network-name> <container-id>
```

Disconnect a container from a network:

```bash
docker network disconnect <network-name> <container-id>
```

Remove a network:

```bash
docker network rm <network-name>
```

## Docker Compose

Start services defined in a `docker-compose.yml`:

```bash
docker-compose up -d
```

Stop services:

```bash
docker-compose down
```

View running services:

```bash
docker-compose ps
```

Rebuild containers:

```bash
docker-compose up --build
```

## Dockerfile

Basic example of a Dockerfile:

```dockerfile
FROM ubuntu:latest
RUN apt-get update && apt-get install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

Build an image using a Dockerfile:

```bash
docker build -t my-nginx .
```

## Docker Logs & Monitoring

View container logs:

```bash
docker logs <container-id>
```

Follow logs in real-time:

```bash
docker logs -f <container-id>
```

Monitor container resource usage:

```bash
docker stats
```

Inspect a container’s details:

```bash
docker inspect <container-id>
```

## Docker Registry

Login to Docker Hub:

```bash
docker login
```

Tag an image for push:

```bash
docker tag <image-name> <dockerhub-username>/<repository>:<tag>
```

Push an image to Docker Hub:

```bash
docker push <dockerhub-username>/<repository>:<tag>
```

Pull an image from a private registry:

```bash
docker pull <registry-url>/<image-name>
```

## Docker Swarm

Initialize a Docker Swarm:

```bash
docker swarm init
```

Create a service in a Swarm:

```bash
docker service create --name <service-name> -p 8080:80 <image-name>
```

List running services:

```bash
docker service ls
```

Scale a service:

```bash
docker service scale <service-name>=3
```

Remove a service:

```bash
docker service rm <service-name>
```