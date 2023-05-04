---
layout: post
title: Install Tailscale
subtitle: Tailscale is a zero config VPN for building secure networks
categories: linux
tags: [linux, vpn]
banner:
  image: /assets/images/banners/tailscale.png
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---

## Ubuntu 22.04(Jammy)
Packages are available for x86 and ARM CPUs, in both 32-bit and 64-bit variants.

* **Add package signing key and repository:**
```bash
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/jammy.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/jammy.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

* **Install Tailscale:**
```bash
sudo apt-get update
sudo apt-get install tailscale
```

* **Connect your machine to your Tailscale network and authenticate in your browser:**
```bash
sudo tailscale up
```

* **You're connected! You can find your Tailscale IPv4 address by running:**
```bash
tailscale ip -4
```
<br />
If the device you added is a server or remotely-accessed device, you may want to consider [disabling key expiry](https://tailscale.com/kb/1028/key-expiry) to prevent the need to periodically re-authenticate.


## CentOS 8/RHEL
* **Add the Tailscale repository and install Tailscale:**
```bash
sudo dnf config-manager --add-repo https://pkgs.tailscale.com/stable/centos/8/tailscale.repo
sudo dnf install tailscale
```

* **Use systemctl to enable and start the service:**
```bash
sudo systemctl enable --now tailscaled
```

* **Connect your machine to your Tailscale network and authenticate in your browser:**
```bash
sudo tailscale up
```

* **You're connected! You can find your Tailscale IPv4 address by running:**
```bash
tailscale ip -4
```
<br />
If the device you added is a server or remotely-accessed device, you may want to consider [disabling key expiry](https://tailscale.com/kb/1028/key-expiry) to prevent the need to periodically re-authenticate.
