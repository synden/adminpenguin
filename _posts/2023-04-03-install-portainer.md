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
## Installation
Download the latest Portainer image:
```bash
sudo docker pull portainer/portainer-ce:latest
```

Create the volume for Portainer data:
```bash
docker volume create portainer_data
``` 

Run Portainer:
```bash
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```
<br />
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


