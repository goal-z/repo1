# Docker, Dockerfile, Docker registry

## Docker 
   - is a framework/ tool to create containers, deploy and run containerized applications
   - provides CLI to interect with docker daemon (background process that runs the containers)
   - docker is also a container run time (responsible for managing low level details of container creation like ns, cgroups, storage volumes and lifecycle of containers
   - provides high level api for interecting with containers ( start, stop, remove )
   - in AKS, docker is not used anymore as container runtime
   - features to manage and orchestrate containers
   - other softwares that prvide container runtimes are - crio, containerD (AKS)

## Image
- is a snapshot (blueprint, genes, dna/rna)-> to create container
- is a prebuilt bundle of code and its dependencies
- is like a template for creating container

## Container
- is the running instance of an image

## Dockerfile
- is a script that has instructions for building an image
- is a plain text file with series of commands executed in order during image buidling
- usually starts with a base image (with a OS) and then run commands to install softwares, add files and configure the image

## How to inatall Docker
- Docker desktop

## Dockerfile code
```
FROM debian:latest 
RUN apt-get update && apt-get -y install curl
CMD ["sleep", "infinity"]
```
## Command to build docker
```
docker build -t my-curl-image .
```
``` 
. means current dir from where you are i.e., look for Dockerfile in the current dir
```
_-t is a tag to name an image_
## To see the image
```
docker images | grep my-curl-image
```
## To create and run a container from the image we have
```
docker run -d --name my-curl-container my-curl-image
```
_-d is to run in detached mode_
_you can see your container running in docker desktop_

## To get inside a running container
```
docker exec my-curl-container curl microsoft.com -v
```
_-v is verbose; here we get inside the container and execute a commnad_

## To see running containers
_go to docker desktop_
OR
```
docker ps
```
## To get inside a running container with id
```
docker exec -it <id> sh
```
_-it is interective mode. after docker ps, place the id number above_
## To see all images
```
docker images
```
## To remove image
```
docker image rm simpplewebsite
```
## To stop the docker container
```
docker stop my-curl-container
```
## To remove the container
```
docker rm my-curl-container
```
## To tag an image
```
docker tag simplewebsite itsarnie/simplewebsite:v1
```
_tag image with an new name (with registry name) in it like repo1/simplewebsite:v1_
## Push image to Docker hub
```
docker push itsarnie/simplewebsite:v1
```
## Docker registry
_Docker hub, ghcr, ACR etc.._

## Start as new container from the image in docker hub
```
docker run -p 80:80 itsarnie/simplewebsite:v1
```
_-p means maps a host port to container port. Host port 80 is mapped to container port 85 meaning incoming traffic on the host port 80 will be forwarded to container port 80 aka port-forwarding. This allows us to access container's app that is listening on port 80 of the host. We can access the container app by http://localhost:80 in the web browser_

_curl localhost_ gives you the response and content of the website
