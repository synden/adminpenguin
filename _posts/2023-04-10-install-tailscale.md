---
layout: post
title: GE-Proton 8-1 Released!
subtitle: Newest GE-Proton mainly pulling in Proton 8 upgrades
categories: linux
tags: [linux, ubuntu, rhel]
banner:
  image: /assets/images/banners/steam.jpg
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---

GE-Proton has a new release out with [8-1](https://github.com/GloriousEggroll/proton-ge-custom/releases/tag/GE-Proton8-1), which is mainly pulling in a whole bunch of improvements from Proton 8 and Proton Experimental.

This is the version of Proton made and supported by the community, for the times where it may work better than the official Valve Proton, but it comes with less testing and may have its own issues.

Here's all that's new:

* All build components rebased to Proton 8 experimental/upstream.
* proton-wine updated to latest experimental.
* wine-staging rebased on top of proton-wine 8.
* proton-ge game patches and pending wine upstream patches rebased on top of proton-wine 8.
* dxvk updated to latest git.
 * vkd3d-proton updated to latest git.
* protonfix: No cutscene audio in Daedalic Games (Memoria, The Night of the Rabbit, A New Beginning - Final Cut) - (thanks marianoag).
* protonfix: Megadimension Neptunia VII - (thanks snaggly).

Some other notes that were included to be aware of:
* FSR is currently disabled again. It needs a massive rebase and same as before I don't know if it's currently possible to rebase/port it over to the new proton 8 build.
* Having the nvapi hack configuration enabled in dxvk.conf seems to crash battlenet. Recommend removing it from the config for existing Lutris battle.net installations and related games.
* Overwatch losing focus after death seems to be fixed.
