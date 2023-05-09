---
layout: post
title: Steam just got better scaling
subtitle: Steamm will now scale better in KDE and GNOME
categories: linux gaming
tags: [linux, gaming, kde, gnome]
banner:
  image: /assets/images/banners/steam.jpg
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---
Valve has released the latest Beta version of Steam on [May 5th](https://store.steampowered.com/news/group/4397053/view/3705943193607193985), which includes several updates to the Steam Client's UI scaling. The company has been working on scaling the UI for a long time, and it's good to see that they have finally made some progress.

According to the release notes, Steam will now use the global scale factor set in KDE or GNOME settings. Specifically, the ```org.gnome.desktop.interface/text-scaling-factor``` will be used. Valve has also re-introduced ```GDK_SCALE``` as a fallback and has added a command-line switch to override it with ```-forcedesktopscaling``` float.

The update also includes fixes to several other issues, such as a big black rectangle appearing in small mode at startup, context menus getting squashed in small mode, and fixing the right trackpad click in the controller binding listening page being bound to left stick click. The changes also apply to the Steam Deck.

Valve also released an update on May 4th, which fixed several issues related to the new UI and Steam Overlay. The changes included fixing issues with navigating forward and back when the client's start page is the Library, tweaking the order and presentation of some items in the account menu, and fixing library artwork not automatically updating in some cases.

The update also fixed issues with download rate display, cursor position in game notes after auto-saving, send trade offer opening in the system browser, and added cloud sync status icon to the Game Notes dialog. The update also fixed some issues related to Linux, such as the file picker dialog not showing any files when browsing for an app icon.

In conclusion, the new design of Steam is starting to feel more stable now, as Valve has fixed many of the issues that came along with the recent major Beta upgrade. It is good to see that Valve is continuously working on improving the Steam Client and addressing user concerns.

Overview of some of the changes:
 **General**
* Fixed issues with navigating forward and back when the client's start page is the Library
* Tweaked the order and presentation of some items in the account menu
* Fixed library artwork not automatically updating in some cases
* Fixed developer, publisher, and franchise links not working in game info panel
* Fixed some formatting issues on downloads page
* Made download throttle setting field honor the bits-per-second/bytes-per-second toggle setting
* Changed default display of download rate to bits per second.
* LED Personalization now has has dedicated sub-page in Controller Calibration page
 * Fixed issue where the cursor position would be reset in Game Notes after auto-saving

**Friends List**
* Fixed Send Trade Offer opening in the system browser
* Fixed Add to Favorites / Remove from Favorites not dismissing the context menu in some instances

**Screenshot Manager**
* Fixed screenshots failing to upload when certain privacy settings were selected
 * Fixed UI glitch when deleting a local screenshot's caption

**In-Game Overlay**
* Added cloud sync status icon to Game Notes dialog. If there's a Steam Cloud conflict, clicking on that icon will display a cloud conflict resolution dialog.
* Fixed issue with Friends List context menu items not opening links in the overlay web browser (e.g. "View Profile" or "Send Trade Offer")
* Fixed issue where some dialogs were not appearing correctly (e.g. Invite Friend to Game, Add Friend, etc.)

**Linux**
* Fixed the file picker dialog not showing any files when browsing for an app icon
* Fixed the Steam Runtime info dialog not showing any information


The list can also be found over at [Steam](https://store.steampowered.com/news/group/4397053/view/3705943193600581522).


