+++
categories = ["docker"]
date = "2021-04-04"
description = "Docker cheatsheet of most commonly used docker commands"
title = "Docker cheatsheet"
+++

Who doesn't like docker, here are some really usefull commands.

## Installation

Steps to install Docker.

### Ubuntu
- Remove existing docker installation: `sudo apt-get purge docker docker-engine docker.io`
- Update System: `sudo apt-get update`
- Install other stuff: `sudo apt-get install apt-transport-https ca-certificates curl software-properties-common`
- Add GPG & Update: `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -` & `sudo apt-get update`
- Add repository:

```bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
- Install: `sudo apt-get install docker-ce`
- Run without sudo: `sudo usermod -aG docker $('whoami')` and restart
- Change default Installation folder

```bash
sudo systemctl stop docker
sudo rm -rf /var/lib/docker
sudo ln -s /media/ravindra/Files/Docker/ /var/lib/docker
```

### List images
```bash
docker images
```
```bash
docker image ls
```

### List containers
```bash
docker container ls
```

### Stop all running containers
```bash
docker stop $(docker ps -a -q)
```

### Docker information
```bash
docker info
```

### List running containers
```bash
docker container ls
```

### List all containers
```bash
docker container ls -all
```

### List all containers in quite mode
```bash
docker container ls -aq
```

### Getting help
```bash
docker container --help
```
```bash
docker image --help
```

### Delete all containers
```bash
docker -rm $(docker ps -a -q)
```
```bash
docker -rm $(docker ps -aq)
```
```bash
docker -rm `docker ps -aq`
```

### Delete all images

```bash
docker -rmi $(docker images -q)
```

```bash
docker -rmi $(docker image ls -q)
```

### Start a stopped container

```bash
docker start <container_name>
```


### Start a stopped container in interactive mode
```bash
docker start -i <container_name>
```


### Stop a running container

```bash
docker stop <container_name>
```


### Run command in a running container
```bash
docker exec <container_name> <command>
```

**Note: You can use command without surrounding it with quotes**


### Attach console to a running container
```bash
docker exec -it <container-id> bash
```