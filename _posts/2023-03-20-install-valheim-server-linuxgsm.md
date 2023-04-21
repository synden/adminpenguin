---
layout: post
title: Install Valheim Server with LinuxGSM
subtitle: Join the wonderful world of Valheim!
categories: linux gaming
tags: [linux, valheim, gaming]
banner:
  image: https://img2.storyblok.com/fit-in/1920x1080/f/157036/1873x1051/d6fcacc246/frostcaveart.png
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
Before installing, you must ensure you have all the dependencies required to run vhserver.

**Ubuntu =< 20.04(64-bit)**
```bash
sudo dpkg --add-architecture i386; sudo apt update; sudo apt install curl wget file tar bzip2 gzip unzip bsdmainutils python3 util-linux ca-certificates binutils bc jq tmux netcat lib32gcc1 lib32stdc++6 libsdl2-2.0-0:i386 steamcmd
```
**Ubuntu => 20.10(64-bit)**
```bash
sudo dpkg --add-architecture i386; sudo apt update; sudo apt install curl wget file tar bzip2 g
```
### Gamedig
GameDig is a recommended additional module that allows LinuxGSM to gather more info from the game server such as current map and connected players to be displayed in details and in logs. It also replaces the default LinuxGSM query module in monitor. To install GameDig follow the steps in the LinuxGSM [documentation](https://docs.linuxgsm.com/requirements/gamedig).


### Install Dependencies Using LinuxGSM
It is possible for LinuxGSM to install dependencies either by having the vhserver user account with sudo access or running the installer as root.<br />
<br />
**user with sudo access**<br />
During the installation if the game server user has sudo permissions LinuxGSM will attempt to install any missing dependencies itself.<br />
<br />
**root user**<br />
if vhserver is already installed run ```./vhserver install``` as root and LinuxGSM will automatically install missing dependencies. 


![valheim_monster](https://img2.storyblok.com/fit-in/1920x1080/f/157036/2560x1440/08ac0f3091/4-cultists.jpg "Monsters in the dark")


## Installation
From the command-line do the following. Ensuring you have also installed the required dependencies.<br />

**Create a user and login:**
```
adduser vhserver
```
**_Note:_** For security best practice, ensure you set a strong password. Random password: Tc3MDcxOTUwO

<br />
**Login as the user:**
```bash
su - vhserver
```
<br />

**Download linuxgsm.sh:**
```bash
wget -O linuxgsm.sh https://linuxgsm.sh && chmod +x linuxgsm.sh && bash linuxgsm.sh vhserver
```
<br />

**Run the installer following the on-screen instructions.**
```bash
./vhserver install
```

![valheim_worl](https://img2.storyblok.com/fit-in/1920x1080/f/157036/2560x1440/ec2eb4f15a/11-loxriding.png "World of Valheim")

