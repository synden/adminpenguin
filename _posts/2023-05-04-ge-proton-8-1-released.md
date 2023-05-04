---
layout: post
title: Update Nextcloud 25 to 26
subtitle: Upgrade your Nextcloud from version 25 to 26
categories: linux self-hosting
tags: [linux, nextcloud]
banner:
  image: /assets/images/banners/nextcloud-bg.jpg
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---
## Update to latest minor version
First you need to upgrade Nextcloud to the latest minor version of Nextcloud. When that's done, you can upgrade to the newest major version.

## Prepare apps for latest version
Before you upgrade to a new major version, you need to make the following changes to your ```appinfo/info.xml``` to allow the next version of Nextcloud for all of your apps. So for Nextcloud 26 you need the following changes to the file:
```bash
<dependencies>
    <nextcloud min-version="23" max-version="26" />
</dependencies>
```

To make the changes to all apps at the same time you could go to the root of your Nextcloud installation and run the following command:
```bash
sed -i -e 's/max-version="25"/max-version="26"/' apps/*/appinfo/info.xml
```
Here you can just change ```26``` to the newer version of Nextcloud.<br />

## Upgrade to latest major version
After this you can go back to the web interface and update to the latest major version of Nextcloud.

Read more over at [Nextcloud](https://docs.nextcloud.com/server/latest/developer_manual/app_publishing_maintenance/app_upgrade_guide/upgrade_to_26.html#)!