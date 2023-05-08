---
layout: post
title: Install Portainer with Docker
subtitle: Quick and easy way to install Portainer with persistent data
categories: linux docker
tags: [linux, docker]
banner:
  image: ../assets/images/banners/tutorials-docker.png
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---
Portainer is a user-friendly graphical interface for managing Docker containers, clusters, and images. It can be installed and updated easily, making it an ideal tool for beginners and experienced users alike. In this article, we will go over the steps to install and update Portainer on a Docker host.

## Install Docker
Before you can install Portainer, you must first have Docker installed on your host system. Docker is a platform that allows you to run and manage containerized applications. To install Docker, follow the instructions for your specific operating system:

* Linux: https://docs.docker.com/engine/install/
* macOS: https://docs.docker.com/docker-for-mac/install/
* Windows: https://docs.docker.com/docker-for-windows/install/

When this is done you can go to the next step.


## Install Portainer
Download the latest Portainer image:
```bash
sudo docker pull portainer/portainer-ce:latest
```

You will need to create a Docker volume to store the Portainer data. This volume will be used to store the Portainer configuration and any other data that is required by the application. To create the volume, run the following command:
```bash
docker volume create portainer_data
``` 

Once you have created the volume, you can run Portainer using the following command:
```bash
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```
This command will start Portainer and map the web interface to port 9000 on your host system. It will also create a container named "portainer" that will automatically restart if it crashes. The "-v" options are used to mount the Docker socket and the data volume that you created before.

After running the above command, you can access the Portainer web interface by navigating to **http://localhost:9000** in your web browser. You will be prompted to create an admin account and choose a password. Once you have done that, you will be logged in and can start managing your Docker containers and images.
<br />

## Update Portainer
Find the container ID with:
```bash
docker ps
```

Then run:
```bash
docker stop CONTAINER-ID
```

Remove old container with:
```bash
docker rm CONTAINER-ID
```

Remove Portainer image with:
```bash
docker rmi portainer/portainer-ce
```

To start Portainer again, run the command you ran when installed Portainer at the beginning.

## Conclusion
Portainer is a powerful tool that makes it easy to manage your Docker containers, clusters, and images. By following the steps outlined in this article, you can install and update Portainer with ease. With Portainer, you can simplify your Docker management tasks and focus on what really matters - building and deploying great applications.

