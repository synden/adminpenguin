---
layout: post
title: Setup Docker on Ubuntu Server
categories: linux
tags: [docker, linux, ubuntu]
banner:
  image: https://images.unsplash.com/photo-1637778352878-f0b46d574a04?ixlib
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---
## Introduction
Docker is a powerful tool for managing and deploying applications in a containerized environment. With Docker, you can easily create, package, and distribute applications, ensuring that they run consistently across different environments. In this blog post, we will guide you through the process of setting up Docker on an Ubuntu server.

## Update and Upgrade the Ubuntu Server
Before installing Docker on your Ubuntu server, you need to ensure that the server is up to date. You can do this by running the following commands:
```bash
sudo apt-get update
sudo apt-get upgrade
```

## Install Docker
Once your Ubuntu server is up to date, you can proceed to install Docker. Docker is available in the Ubuntu package repository, so you can install it using the following command:
```bash
sudo apt-get install docker.io
```
This will install the Docker engine and all the necessary dependencies.

> **_Note:_**  You could install either ```docker.io``` or ```docker-ce```.

- ```docker.io``` does it the Debian (or Ubuntu) way: Each external dependency is a separate package that can and will be updated independently.

- ```docker-ce``` does it the Go way: All dependencies are pulled into the source tree before the build, and the whole thing forms one single package afterwards. So you always update Docker with all its dependencies at once.

Docker is now installed and you can check if it's running:
```bash
sudo systemctl status docker
```

If not, start Docker and enable it at boot with:
```bash
sudo systemctl start docker
sudo systemctl enable docker
```


### Verify the Docker Installtion
After installing Docker, you can verify that the installation was successful by running the following command:
```bash
sudo docker run hello-world
```
This command will download and run a simple Docker container, and output a message that confirms that Docker is installed and working correctly.

## Manage Docker as a Non-Root User
By default, Docker requires root privileges to run, which can be a security risk. To avoid this, add your user to the docker group:
```bash
sudo usermod -aG docker $USER
```
> **_Note:_** that you will need to log out and log back in for the changes to take effect.

If the group doesn't exists, you can create it with the following command and then run the other command again:
```bash
sudo groupadd docker
```

## Using Docker
Once you have Docker installed and configured on your Ubuntu server, you can start using it to create and manage containers. To create a new container, you can use the ``docker run`` command, followed by the name of the container image that you want to use.

For example, to create a new container based on the latest version of the Ubuntu image, you can use the following command:
```bash
sudo docker run -it ubuntu:latest /bin/bash
```
This will start a new container and launch the bash shell. You can then install any additional packages or software that you need inside the container.

## Conclusion
In this blog post, we have shown you how to set up Docker on an Ubuntu server, and how to create and manage containers. Docker is a powerful tool for managing and deploying applications, and can greatly simplify the process of deploying applications across different environments. With these steps, you should now be able to set up Docker on your own Ubuntu server and start using it to manage your applications.
