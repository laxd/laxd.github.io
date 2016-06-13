---
layout: default
title: "Tunneling over SSH"
---
Example of tunneling a port from localhost to example.com
ssh -L 80:reddit.com:80 example.com

Example of tunneling a port from current machine (external addresses too) to example.com
ssh -L 0.0.0.0:80:reddit.com:80 example.com

e.g. if current server is myserver.com, a request to myserver.com:80 would be redirected to reddit.com:80 through example.com:80
