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

