# Docker and Kubernetes
 This repository contain the information of the course: Docker and Kubernetes

## Docker ecosystem

- Docker client
- Docker server
- Docker machine
- Docker images
- Docker hub
- Docker compose
- Docker swarm

Check Docker version

```
Docker version
```

Check correct installation

```
Docker run hello-world
```

### Namespacing

Isolating resources per process (or group of processes)

- Processes
- Hard drive
- Network
- Users
- HostNames
- Inter process comunication

### Control Groups (cgroups)

Limit amount of resources used per process

- Memory
- CPU usage
- HD I/O
- Network bandwith

# Commands

- Create docker container

```
docker create <image-name>
```

- Start docker container

```
docker start <container-id>
```

- Start docker container and show log in terminal

```
docker start -a <container-id>
```

- Running Docker container

```
docker run <image-name>
```

- Override default startup command

```
docker run <image-name> command
```
Note: docker run = docker create + docker start

- Listing running containers

```
docker ps
```

- Show all containers

```
docker ps -a
```

- Remove all stopped containers

```
docker system prune
```

- To show logs of a container

```
docker logs <container-id>
```

- Stop container

```
docker stop <container-id>
```

- Kills container

```
docker kill <container-id>
```

## Multi command containers

- Enter in executing container

```
docker exec -it <container-id> <command>
```

Example: Run redis container and interact with redis-cli

```
docker run redis
```
```
docker exec -it <container-redis-id> redis-cli
```

- There are 3 channels to communicate with containers using cli

+ STDIN
+ STDOUT
+ STDERR

- To execute linux commands in running container

```
docker exec -it <container-id> sh
```

- To run container with interactive sh

```
docker run -it <image-id> sh
```
