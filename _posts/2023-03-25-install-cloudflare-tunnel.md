---
layout: post
title: Install Cloudflare Tunnel on Ubuntu
subtitle: No more open ports with Cloudflare Tunnel
categories: linux
tags: [linux, bash, ubuntu]
banner:
  image: https://www.cloudflare.com/static/61dea7db2b4d1b5325898dd0e25ce458/tunnel-hero-illustration.svg
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---

Cloudflare Tunnel is a tool that allows you to expose your local web server to the internet securely. This tool is useful for developers who want to test their web applications on a remote server or want to access their local web server from a remote location. In this blog post, we will guide you through the process of installing Cloudflare Tunnel on an Ubuntu server.

## Install Cloudflare Tunnel

The first step is to download the Cloudflare Tunnel binary from the official website. You can download the binary from the [following link](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/installation).

Once you have downloaded the binary, you need to extract it to a directory on your server. You can extract the binary using the following command:
```bash
tar -zxvf cloudflared-stable-linux-amd64.tgz
```
This will extract the binary to a directory named ```cloudflared```.


## Configure Cloudflare Tunnel

After extracting the binary, you need to configure Cloudflare Tunnel to connect to your Cloudflare account. To do this, you need to create a configuration file named ```config.yml``` in the ```cloudflared``` directory. You can create this file using the following command:
```bash
nano cloudflared/config.yml
``` 
In the configuration file, you need to add your Cloudflare account credentials. Here is an example of what the configuration file should look like:
```bash
tunnel: your_tunnel_name
credentials-file: /etc/cloudflared/creds.json

ingress:
  - hostname: your_subdomain.your_domain.com
    service: http://localhost:8080
  - service: http_status:404
```
In the above example, you need to replace ```your_tunnel_name```, ```your_subdomain```, and ```your_domain.com``` with your own values. Also, make sure to change the **service** parameter to the URL of your local web server.


## Create Cloudflare Credentials
Next, you need to create Cloudflare credentials for your Tunnel. To do this, you need to login to your Cloudflare account and go to the **API Tokens** page. From there, click on **Create Token** and select the **Edit Cloudflare Workers** option.

In the permissions section, select the following options:
* Account: Zone: Read
* Account: Zone: DNS: Edit
* Workers Scripts: Edit

After selecting these options, click on **Create Token**. This will generate a token that you can use to authenticate Cloudflare Tunnel.

## Save Cloudflare Credentials
Once you have created the Cloudflare credentials, you need to save them in a file named ```creds.json```. You can save the credentials using the following command:

```bash
nano /etc/cloudflared/creds.json
```
In the file, you need to add the following JSON object:
```json
{
    "AccountTag": "your_account_tag",
    "APIToken": "your_api_token"
}
```
In the above example, replace ```your_account_tag``` and ```your_api_token``` with your own values.

## Start Cloudflare Tunnel
Finally, you can start Cloudflare Tunnel using the following command:
```bash
./cloudflared tunnel run
```

This will start the Cloudflare Tunnel and connect it to your Cloudflare account. You should now be able to access your local web server using the URL ```https://your_subdomain.your_domain.com```.

## Conclusion
In this blog post, we have shown you how to install Cloudflare Tunnel on an Ubuntu server. By following these steps, you should be able to expose your local web server to the internet securely. If you encounter any issues, you can refer to the official


