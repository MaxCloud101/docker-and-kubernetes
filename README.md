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

Docker use Namespacing and Control Groups

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
docker run <image-name> <command>
```

- Run docker as a daemon

```
docker run -d redis
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

## Building custom images

- To build a image

```
docker build .
```

- To biuld image with tag

```
docker build -t docker-id/project-name/verion . 
```

## Manual image generation

- To create image from docker-container

```
docker commit -c 'CMD <command>' <container-id>
```

## Docker compose

- To run docker compose

```
docker-compose up
```

- To build and run docker compose

```
docker-compose up --build
```

- Docker compose as daemon

```
docker-compose up -d
```

- To stop docker compose

```
docker-compose down
```

- To list docker compose

```
docker-compose ps
```

Docker compose restart policies

- No: Never attempt restart this
- Always: If this container stop for any reason always attempt to restart it
- on-failure: Only restart if the container stop with an error code
- unless-stopped: Always restart unless we (the developer) forcibly stop it

# Kubernetes

There are two parts:

- minikube: manage clusters in local
- kubectl: mana container in local and produccion

## Api versions and objects

### apiVersion: v1

- ComponentStatus
- configMap
- Endpoints
- Event
- Namespace
- Pod

### apiVersion: apps/v1

- ControllerRevision
- StatefulSet

## Pods

## Services

- ClusterIp
- NodePort: Export container outside the world, (Usually only for development)
- LoadBalancer
- Ingress

## Minikube

- To run

```
minikube start
```

- Check if is running

```
minikube status
```

- Get ip

```
minikube ip
```

## Kubectl

- Check if is correctly installed

```
kubectl cluster-info
```

- Feed a config file to Kubectl

```
kubectl apply -f <filename>
```

- Print status of all runing pods

```
kubectl get pods
```

- Print status of all runing pods with more information

```
kubectl get pods -o wide
```

- Print status of all runing deployments

```
kubectl get deployments
```

- Print status of all runing services

```
kubectl get services
```

- Get detailed info

```
kubectl describe <object-type> <object-name>
```

- Remove an object

```
kubectl delete -f <filename>
```

- Imperative command to update an image

```
kubectl set image <object-type> / <object-name> <container-name>=<container-image>:<container-version>
```
```
kubectl set image deployment/client-deployment clent=damianenko/multi-client:v5
```
## Ways to deploy container

- Delete and recreate pods (Bad solution)
- Tag image with versions and update config file (Medium solution)
- Use an imperative command

## Configure docker client to use minikube VM

```
eval $(minikube docker-env)
```
