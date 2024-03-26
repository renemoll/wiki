---
title: Git
description: 
published: true
date: 2024-03-26T13:42:29.771Z
tags: 
editor: markdown
dateCreated: 2024-03-26T13:42:29.771Z
---

# Git

Config with multiple personalities (logins)

```bash
[user]
        name = René Moll
        email = rene.moll@XXXX.com
        signingkey = ~/.ssh/id_rene_pub
[includeIf "gitdir:~/personal/"]
    path = .gitconfig.personal
```

`.gitconfig.personal`:

```bash
[user]
name = René Moll
email = github@r-moll.nl
signingkey = ~/.ssh/id_rene_personal_pub
```
