---
layout: post
title: Update RHEL 8.3 to 8.4
subtitle: Time to upgrade RHEL 8.3 to 8.4 with these steps
categories: linux
tags: [linux, rhel]
banner:
  image: ../assets/images/banners/redhat.jpg
  opacity: 0.618
  background: "#000"
  height: "90vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---
Red Hat Enterprise Linux (RHEL) 8.4 released. This version includes updates and various improvements for developers, hybrid cloud, edge deployments and more.

New software and feature in RHEL 8.4:
* Python 3.9
* Redis 6
* PostgreSQL 13
* MariaDB 10.5
* GCC 10
* LLVM 11
* Rust 1.49
* Go 1.15.7
* Intel Tiger Lake GPUs are now supported which includes Intel UHD graphics and Intel Xe integrated GPUs.
 
> **Warning**
> Make sure you keep verified RHEL 8.x backups before performing minor or significant RHEL version upgrades. The author or nixCraft is not responsible for data loss.


## Update from 8.3 to 8.4
Now it's time to upgrade. Follow these steps:
* Open the terminal application and then type the following commands. Another option is to log in using ssh
* Login as the root user. For example: ```ssh ec2-user@rhel-8-ec2-box```
* Check for updates using the ```sudo dnf check-update``` command
* Update the system using the ```sudo dnf update``` command
* Reboot the server/box using the ```sudo reboot``` command
* Verify new kernel and updates

Typically I use Ansible to upgrade and update RHEL boxes running at AWS or Google cloud. Another option is to deploy updated images and get rid of older instances. Let us see all commands and steps in details.

### 1. Note down kernel version
Use any of the following commands:
```bash
uname -a
uname -r
cat /etc/os-release
```

### 2. Backups
Make a backup - it cannot be stressed enough how important it is to backup your system before you do this.

## 3. Check for updates
```bash
sudo dnf check-update
```

### 4. Run the upgrade
```bash
sudo dnf upgrade
```
Do through the packages before you press Yes to upgrade. Just to be safe.


### 5. Reboot the host
```bash
sudo reboot
## OR ##
sudo shutdown -r now
```


### 6. Verify the upgrade
```bash
uname -a
uname -r
cat /etc/os-release
tail -f /var/log/logfilename
dmesg |grep -i 'err|warn|cri'
ss -tulpn
```

## Conclusion
The new RHEL 8.4 available to all active RHEL subscriptions, including the no-cost option via the Red Hat Customer Portal/RHN. Updated developer tools such as MariaDB and Python are great too. Apart from that, we get updated container support and container security with SELinux. Podman 3 (rootless Docker) also brings many enhancements for container workloads, including automatic container image updates. So no more outdated OpenSSL inside your container via UBI (Red Hat Universal Base Image).
