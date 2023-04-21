---
layout: post
title: Setting up SSH Keys in Linux
subtitle: Secure your Linux server with key authentication
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

SSH (Secure Shell) is a widely-used protocol for securely connecting to remote systems over an unsecured network. Setting up SSH keys allows you to connect to remote systems without having to enter a password each time you log in. In this article, we will discuss how to set up SSH keys and use them to connect to remote systems via SSH.

 

## Setting Up SSH Keys
To set up SSH keys, follow these steps:
Open a terminal window on your local machine. Enter the following command to generate a new SSH key:
```bash
ssh-keygen -t rsa -b 4096
```
This command generates a new RSA key pair with a key size of 4096 bits. Press Enter when prompted to accept the default file name and location for the key.

Enter a passphrase for the key when prompted. The passphrase adds an extra layer of security to your key. Make sure to choose a strong passphrase and keep it secure.

Once the key pair is generated, you should see two files in your local machine's ```.ssh``` directory:<br />
```id_rsa``` - The private key<br />
```id_rsa.pub``` - The public key<br />
 

## Connecting to Remote Systems
To connect to a remote system with SSH keys, follow these steps:
Copy your public key to the remote system by running the following command:
```bash
ssh-copy-id username@remote_host
```
Replace "**username**" with your username on the remote system, and "**remote_host**" with the IP address or hostname of the remote system.

Enter your password when prompted.
Once the key is copied, you can connect to the remote system using SSH without entering a password:
```bash
ssh username@remote_host
```
This command will log you in to the remote system using your SSH key. If you set a passphrase for your key, you will be prompted to enter it.

## Conclusion
Setting up SSH keys allows you to securely connect to remote systems without having to enter a password each time you log in. In this article, we discussed how to set up SSH keys and use them to connect to remote systems via SSH. By following these steps, you can increase the security of your remote connections and make it easier to manage multiple systems.
