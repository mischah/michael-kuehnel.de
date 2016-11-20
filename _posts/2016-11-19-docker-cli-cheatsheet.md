---
layout: post
lang: en_GB
title:  "Cheat Sheet: Docker CLI"
date:   2016-11-19 16:45:00
category: Docker
tags: "Docker, Cheat Sheet, CLI, Terminal, Command line interface"
image: "/assets/img/docker-logo.svg"
excerpt: "I’m new to Docker. So this cheatsheet is primarily for me to help to remember commands for handling containers as well as images."
disqusIdentifier: 2016-11-19-docker-cli-cheatsheet
---

<div class="float-container">
    <img src="{{page.image}}" alt="" class="float-left">
    <div>
        <p>
          {{page.excerpt}}
        </p>
    </div>
</div>

See [Docker command line reference](https://docs.docker.com/engine/reference/commandline/) for the whole reference.

# Containers

## Listing containers

```bash

# List running containers 
docker ps

# List all containers
docker ps -a	

```

## Starting/Stopping containers

```bash
# Start 
docker start containerName

# Stop
docker stop containerName
```

## Removing containers

```bash
# Remove container 
docker rm containerName

# Stop and remove container
docker rm -f containerName

# Remove all exited containers
docker rm -v $(docker ps -a -q -f status=exited)
```

## Running commands in new containers

```bash 
docker run imageName command arguments

# Example
docker run docker/whalesay cowsay Hello

# Assign a name to the container
docker run --name myName docker/whalesay cowsay Hello

# Run with a specific tag of an image
docker run node:6.9.1 node --version

# Run container in background
docker run -d -p 80:80 --name webserver nginx
```

See [Docker run reference](https://docs.docker.com/engine/reference/run/) for more …

# Images

## Listing local images

```bash
docker images
```

## Removing images

```bash
docker rmi imageName

# Remove unwanted dangling images
docker rmi $(docker images -f "dangling=true" -q)
```

## Searching for images 

```bash
# Search the Docker Hub for images
docker search searchWord
```

## Pulling images

```bash
docker pull imageName

# Pull a specific tag
docker pull imageName:tag

# Example: Get a specific node version
docker pull node:6.9.1
```

## Building image from Dockerfile

```bash
docker build .

# Name the image
docker build -t imageName .

# Tag the image
docker build -t imageName:1.0.0 .
```

See [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) in addition.
