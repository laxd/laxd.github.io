---
layout: default
title: "Wiping a Hard Drive with Linux"
categories: linux
---

* You usually want to use shred
* When you can't use shred (no install rights) you can use dd
* Source either /dev/urandom or /dev/zero
* This WILL use up 100% of one of your CPU cores
* Unless you spawn multiple processes to fill up your HDD faster
