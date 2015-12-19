---
layout: default
title: "Arch Linux Arm setup on a Raspberry Pi Zero"
categories: raspberrypi
---

Initial Setup
-------------

instructions for flashing the SD card can be found here:

http://archlinuxarm.org/platforms/armv6/raspberry-pi

These instructions can't be followed from windows machines, so you need to either boot into a linux VM or flash the SD card from another raspberry pi if you don't have a linux PC hanging around.


Enabling Wifi
-------------

When you first switch on your Pi0, you may be surprised to see that wifi is not enabled by default. This is due to the arch philosophy of being a simple system with the least amount of assumptions (not everyone will be using wifi). Enabling can be troublesome if you don't have a USB hub as there is only a single (micro) USB slot available. To make matters worse, the libraries required are not installed either, as evidenced when you first try to enable wifi and get a nasty error message telling you about the fact that wpa-supplicant is not installed.

At first I figured that's fine, just install it using pacman!

`pacman -S wpa-supplicant`

But, of course, this failed due to not having an internet connection, and there being no ethernet port to temporarily use either. 

The solution, I found, was to install the required files from the arch repository manually. For the raspberry pi 0, this repository is located at http://os.archlinuxarm.org/armv6h/core/

To install the packages, we need to mount either a USB stick or the raspberry pi's sd card into a host computer and download these files:

libnl-3.2.26-1-armv6h.pkg.tar.xz
wireless_tools-30.pre9-1-armv6h.pkg.tar.xz
wpa_supplicant-1:2.5-1-armv6h.pkg.tar.xz
dialog-1:1.2_20150920-1-armv6h.pkg.tar.xz
netctl-1.11-1-any.pkg.tar.xz

(The versions may have changed since I wrote this)

On linux, you can execute the following commands to download all of these:

```
wget http://os.archlinuxarm.org/armv6h/core/netctl-1.11-1-any.pkg.tar.xz
wget http://os.archlinuxarm.org/armv6h/core/libnl-3.2.26-1-armv6h.pkg.tar.xz
wget http://os.archlinuxarm.org/armv6h/core/dialog-1:1.2_20150920-1-armv6h.pkg.tar.xz
wget http://os.archlinuxarm.org/armv6h/core/wpa_supplicant-1:2.5-1-armv6h.pkg.tar.xz
wget http://os.archlinuxarm.org/armv6h/core/wireless_tools-30.pre9-1-armv6h.pkg.tar.xz
```

Copy these to the Pi and execute `pacman -U *.tar.xz` to install them. Once you've done this, you should be able to finish setting up your Wifi connection.

Connecting to Wifi
------------
