---
layout: post
title: Install Valheim Server on Ubuntu
subtitle: Join the wonderful world of Valheim!
categories: linux gaming
tags: [linux, valheim, ubuntu, gaming]
banner:
  image: ../assets/images/banners/valheim-cave.png
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---
Valheim is an online multiplayer survival game that has taken the gaming world by storm. If you're a fan of the game and want to host your own Valheim server on Ubuntu, this article will guide you through the installation process.

![sail_viking](https://img2.storyblok.com/fit-in/1920x1080/f/157036/2560x1440/1bde3f3288/1-sailing.jpg "Sail, Viking!")


## Prerequisites
Before we begin, you will need the following:

* A server running Ubuntu 18.04 or higher
* A non-root user with sudo privileges
* Basic knowledge of the Linux command line

## Step 1 - Install Dependencies
To run a Valheim server on Ubuntu, you will need to install the following dependencies:
```bash
sudo apt update
sudo apt install -y curl unzip screen lib32gcc1
```

![valheim_monster](https://img2.storyblok.com/fit-in/1920x1080/f/157036/2560x1440/08ac0f3091/4-cultists.jpg "Monsters in the dark")


## Step 2 - Download and Install SteamCMD
Valheim is available on Steam, so we need to download and install SteamCMD, a command-line version of the Steam client, to manage our server.
```bash
mkdir ~/steamcmd && cd ~/steamcmd
curl -sqL "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz" | tar zxvf -
```
 
## Step 3 - Install and Configure the Valheim Server
Once SteamCMD is installed, we can use it to install and configure the Valheim server.
```bash
cd ~/steamcmd
./steamcmd.sh +login anonymous +force_install_dir ~/valheim +app_update 896660 validate +exit
```
This command will download and install the Valheim server to the ~/valheim directory.


## Step 4 - Configure the Server
Now that the Valheim server is installed, we need to configure it by creating a new start_server.sh script. This script will start the Valheim server with the desired settings.

```bash
nano ~/valheim/start_server.sh
```
Copy and paste the following script into the file:
```bash
#!/bin/bash

export templdpath=$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=./linux64:$LD_LIBRARY_PATH
export SteamAppId=892970

./valheim_server.x86_64 -name "My server" -port 2456 -world "Dedicated" -password "mypassword" -savedir "/home/username/valheim/saves"
export LD_LIBRARY_PATH=$templdpath
```
Make sure to replace My server, mypassword, and username with your desired server name, password, and username respectively.

Save and close the file by pressing Ctrl+X, then Y, then Enter.

## Step 5 - Start the Server
Now that the server is configured, we can start it using the following command:

```bash
cd ~/valheim && ./start_server.sh
```
This command will start the Valheim server with the settings specified in the start_server.sh script.


## Step 6 - Connect to the Server

Once the server is running, you can connect to it from the Valheim game client. In the game menu, select "Join Game" and enter the server IP address followed by the port number, separated by a colon.

For example: ```192.168.1.100:2456```

## Conclusion
Congratulations! You now have a Valheim server up and running on your Ubuntu server. With this guide, you can easily install and configure your own Valheim server to enjoy the game with your friends. Remember to keep the server updated and secure by regularly installing updates and setting up firewalls. Happy gaming!

![valheim_worl](https://img2.storyblok.com/fit-in/1920x1080/f/157036/2560x1440/ec2eb4f15a/11-loxriding.png "World of Valheim")

