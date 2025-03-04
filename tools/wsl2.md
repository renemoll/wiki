---
title: WSL2
description: 
published: true
date: 2025-03-04T08:01:17.049Z
tags: 
editor: markdown
dateCreated: 2024-03-26T11:44:47.091Z
---

[How to set up working X11 forwarding on WSL2](https://stackoverflow.com/questions/61110603/how-to-set-up-working-x11-forwarding-on-wsl2)


`.wslconfig`:
```
[wsl2]
memory=3GB   # Limits VM memory in WSL 2 up to 3GB
processors=2 # Makes the WSL 2 VM use two virtual processors

[experimental]
autoMemoryReclaim=gradual
sparseVhd=true
```
Source: [Windows Subsystem for Linux September 2023 update](https://devblogs.microsoft.com/commandline/windows-subsystem-for-linux-september-2023-update/)
