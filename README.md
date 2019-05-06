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

## Kubernetes Objects
### 1 Pods

### 2 Services

Setup a networking in a kubernetes cluster

- ClusterIp: Export containers into cluster
- NodePort: Export container outside the world, (Usually only for development)
- LoadBalancer: Legacy way of getting network traffic into a cluster
- Ingress: Expose a set of services outside the world

### 3 Deployments

### 4 Secrets

Securely stores pieces of information

## Kubernetes volume types

- Volume: Store data at pod level, this can be access by other pods, but if the entired pod is deleted or recreated, the volume is erased.
- Persistent volume: Store data out of the pods, This is deleted when the administrator specifies it
- Persistent volume Claim: It is an advertising of volume options.
  - Statically provisioned persistent volume: Its exists
  - Dinamically provisioned persistent volume: Created when ask for it

## Volume access modes

- ReadWriteOne: Can be used by a single node
- ReadOnlyMany: Multiple nodes can read from this
- ReadWriteMAny: Can be read and written to by many nodes

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

- To review the dashboard

```
minikube dashboard
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

- Print status of all persisten volumes

```
kubectl get pv
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

- Get Storage classes

```
kubectl get storageclass
```

```
kubectl describe storageclass
```

- To create a secret object

```
kubectl create secret <secret-type> <secret_name> --from-literal key=value
```
where secret-type = generic, docker-registry, tls

```
kubectl create secret generic pgpassword --from-literal PGPASSWORD=12345asdf
```

## Ways to deploy container

- Delete and recreate pods (Bad solution)
- Tag image with versions and update config file (Medium solution)
- Use an imperative command

## Configure docker client to use minikube VM

```
eval $(minikube docker-env)
```

## Ingress nginx

https://kubernetes.github.io/ingress-nginx/

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/mandatory.yaml
```
