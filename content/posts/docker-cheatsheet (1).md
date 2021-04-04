---
title: "Docker Cheatsheet"
date: 2019-10-18T00:23:00+05:30
description: "Docker cheatsheet is a list of most commonly used docker commands to help you with web development stuff"
tags: [docker, php, apache, mysql]
category: [DevOps, Docker]
---

Who doesn't like docker, here are some really useful commands.

## Installation
Install docker by following official guide.
https://docs.docker.com/install/

- Run without sudo: `sudo usermod -aG docker $('whoami')` and restart
- Change default Installation folder

```bash
# Changing default installation folder is optional, I like keeping it separate from root partition
# because downloading multiple files may fill your root partition
sudo systemctl stop docker
sudo rm -rf /var/lib/docker
sudo ln -s /media/ravindra/Files/Docker/ /var/lib/docker
```

### List images
```bash
docker images # it is an alias to docker image ls
docker image ls
```

### List containers
```bash
# Show all running containers
docker container ls

# Show all containers including stopped ones
docker container ls -a
```

### Stop all running containers
```bash
docker stop $(docker ps -a -q)
```

### Docker information
```bash
docker info
```

### Getting help
```bash
docker container --help
docker image --help
```

### Delete all containers
```bash
docker -rm $(docker ps -a -q)
docker -rm $(docker ps -aq)
```

### Delete all images

```bash
docker -rmi $(docker images -q)
docker -rmi $(docker image ls -q)
```

### Start a stopped container

```bash
# Non interactive mode
docker start <container_name>

# Interactive mode/cli
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

### Run a container from an image
```bash
docker run <image_name>
```

Execute command in a running container
```bash
docker exec -it <container> /bin/bash 
# i - interactive
# t - attach to a tty
```

### Some Useful Commands For Quick Reference

Pull an image for PHP 5
```bash
docker pull php:5.6.40-apache
# There are many versions, {version}-apache is debian OS with apache server
```

To run php5.6 with apache in current folder run.
```bash
docker run -d -p 127.0.0.1:80:80 --name php56 --restart=unless-stopped -v "$PWD":/var/www/html php:5.6.40-apache
# --name:       Container name
# --restart:    Restart condition
# -d:           Run container in background
# -v:           Volume host:guest mount
```

You can run above command without pulling php5 and it will pull automatically.
It will also create a container with name php56

To access container type
```bash
docker exec -it php56 /bin/bash

# To Enable Rewrite module type
a2enmode rewrite

# To restart server type 
service apache2 restart
```

To remove php56 container
```bash
# This will stop running container, similar to shutting down VM
docker container stop php56

# This will remove stopped container
docker container rm php56
```

You can run multiple PHP versions at same time using docker, this is an example to show that

First create a file with name index.php in current folder and put some content into it, I would say phpinfo statement would be nice.

```bash
# Run a PHP5.6 Container on port 8056
docker run -d -p 127.0.0.1:8056:80 --name php56 --restart=unless-stopped -v "$PWD":/var/www/html php:5.6.40-apache

# Run a PHP7.2 Container on port 8072
docker run -d -p 127.0.0.1:8072:80 --name php72 --restart=unless-stopped -v "$PWD":/var/www/html php:7.2-apache


# Run a PHP7.4 Container on port 8074
docker run -d -p 127.0.0.1:8074:80 --name php74 --restart=unless-stopped -v "$PWD":/var/www/html php:7.4.0RC1-apache

# Run a php latest container on port 8000
docker run -d -p 127.0.0.1:8000:80 --name php80 --restart=unless-stopped -v "$PWD":/var/www/html php:apache
```

You should enable mysql port mapping if you are using docker to run different versions of PHP


Pull MySQL server from docker repository

```bash
docker pull mysql/mysql-server:8.0
# Pull 8.0 version of MySQL
```

Run a container named `mysql8` from mysql
```bash
# Run if you want to access it from docker only
docker run --name=mysql8 -d mysql/mysql-server:8.0

# Run if you want to access it from localhost
# NOTE: Don't try this command, you may face some problem in setting password
docker run --name=mysql8 -p 127.0.0.1:3306:3306 -d mysql/mysql-server:8.0
# -p:   Publish guest port to host

# Start container with pre defined mysql password
docker run --name=mysql8 -p 127.0.0.1:3306:3306 -e MYSQL_ROOT_PASSWORD=password -d mysql/mysql-server:8.0
```

Now type the following command and note your password
```bash
shell> docker logs mysql8 2>&1 | grep 'GENERATED'
```

Connect to mysql server in docker
```bash
docker exec -it mysql8 mysql -uroot -p
```

Now set a new password for root
```mysql
# Replace password with password you want to set for root
ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';

# Allow remote access to MySQL Server
# You can also create another user other than root
create user 'root'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';
EXIT
```


## Running a ubuntu machine in docker and have fun with it

Simple examples

### Pull ubuntu
```bash
docker pull ubuntu
```

### Start a container and expose port 80, 3306
```
docker run --name myubuntu -p 127.0.0.1:80:80 -p 127.0.0.1:3306:3306 -it ubuntu /bin/bash
```

What ever you change, make sure command ends with `ubuntu /bin/bash`

### First install very basic tools
```bash
apt update
apt upgrade -y
apt install curl wget
```

### Run GUI apps from docker

Create a dockerfile
```Dockerfile
FROM ubuntu
RUN apt update &&
RUN apt install -y x11-apps
CMD ["/usr/bin/xeyes"]
```

Build an image
```bash
docker build -t eyes .
```

Run the program
```bash
docker run --net=host --env="DISPLAY" --volume="$HOME/.Xauthority:/root/.Xauthority:rw" eyes
```