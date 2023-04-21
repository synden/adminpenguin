---
layout: post
title: Export Docker Container to Stack
subtitle: Generate a docker-compose yaml definition from a docker container.
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

This will use a Docker container called [docker-autocompose](https://github.com/Red5d/docker-autocompose) to export a current Docker container and its settings to YAML text so you can past it into a stack inside Portainer.

Use the new image to generate a docker-compose file from a running container or a list of space-separated container names or ids. This one is the easiest to start with:
```bash
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose <container-name-or-id> <additional-names-or-ids>...
```
<br />

To print out all containers in a docker-compose format:
```bash
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose $(docker ps -aq)
```

And this will output a docker-compose compatible yaml structure.
<br />
<br />
<br />

Here are some examples:

```bash
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose mariadb
```

```bash
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose nextcloud
```

```bash
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose handbrake
```

After running this or these commands, you can take the output and create a stack inside Portainer for example to create a new container. You can also change what you want to have in the stack. Maybe you don't want all the settings, just the basic. Then remove everything you don't need and past it into the stack.

If you want to watch a video on how to do it, you want watch [this](https://www.youtube.com/watch?v=-ttZjGBkLL8) on YouTube from the amazing DB Tech.
