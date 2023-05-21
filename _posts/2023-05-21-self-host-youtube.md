---
layout: post
title: Tube Archivist - Self-host your own YouTube videos
subtitle: How I Control What Media My Kids Watch Using Tube Archivist
categories: self-hosting
tags: [linux, self-hosting, docker]
banner:
  image: /assets/images/banners/tube-archivist-logo.jpg
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---
## Introduction
Manage your kids' viewing choices at home effortlessly with Tube Archivist, your very own self-hosted YouTube media server. When you work from home, it's crucial to have a peaceful environment, and providing suitable content for your children during work hours is key. However, letting them roam freely on YouTube wasn't an option for us. We needed a solution that granted us greater control, ensuring they only watched appropriate videos.

Introducing [Tube Archivist](https://github.com/tubearchivist/tubearchivist), the game-changer in our household when it comes to kids' content consumption. Tube Archivist is a convenient application that allows you to download and privately enjoy your favorite YouTube subscriptions and channels, free from ads and irrelevant content. It also serves as a fantastic way to keep your kids entertained while you focus on your work.

With Tube Archivist, you have the flexibility to select which channels you wish to download. You can opt for manual or automatic downloads based on your preferences. Personally, what sold me on this application was the ability to browse the channels and see the latest videos available. Tube Archivist provides complete control over the content you choose to save.

![tube-archivist](/assets/images/banners/tube-archivist-2.png "TubeArchivist")

You can access the downloaded videos through popular media servers such as Plex, Emby, or even Tube Archivist's own built-in video player. All of this is made possible by hosting Tube Archivist on my Proxmox server using Docker.

Whether you're a parent seeking better control over your children's viewing habits or someone interested in self-hosting and searching for an application like Tube Archivist for different purposes, this is the solution you've been looking for.

## Installation
You can find the installation from the author [here](https://github.com/tubearchivist/tubearchivist#installing).

For minimal system requirements, the Tube Archivist stack needs around 2GB of available memory for a small testing setup and around 4GB of available memory for a mid to large sized installation. Minimal with dual core with 4 threads, better quad core plus. This project requires docker. Ensure it is installed and running on your system.

I used their docker-compose file and changed it after my needs:
```yaml
version: '3.3'

services:
  tubearchivist:
    container_name: tubearchivist
    restart: unless-stopped
    image: bbilly1/tubearchivist
    ports:
      - 8000:8000
    volumes:
      - media:/youtube
      - cache:/cache
    environment:
      - ES_URL=http://archivist-es:9200     # needs protocol e.g. http and port
      - REDIS_HOST=archivist-redis          # don't add protocol
      - HOST_UID=1000
      - HOST_GID=1000
      - TA_HOST=tubearchivist.local         # set your host name
      - TA_USERNAME=tubearchivist           # your initial TA credentials
      - TA_PASSWORD=verysecret              # your initial TA credentials
      - ELASTIC_PASSWORD=verysecret         # set password for Elasticsearch
      - TZ=America/New_York                 # set your time zone
    depends_on:
      - archivist-es
      - archivist-redis
  archivist-redis:
    image: redis/redis-stack-server
    container_name: archivist-redis
    restart: unless-stopped
    expose:
      - "6379"
    volumes:
      - redis:/data
    depends_on:
      - archivist-es
  archivist-es:
    image: bbilly1/tubearchivist-es         # only for amd64, or use official es 8.7.0
    container_name: archivist-es
    restart: unless-stopped
    environment:
      - "ELASTIC_PASSWORD=verysecret"       # matching Elasticsearch password
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
      - "xpack.security.enabled=true"
      - "discovery.type=single-node"
      - "path.repo=/usr/share/elasticsearch/data/snapshot"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - es:/usr/share/elasticsearch/data    # check for permission error when using bind mount, see readme
    expose:
      - "9200"

volumes:
  media:
  cache:
  redis:
  es:
```