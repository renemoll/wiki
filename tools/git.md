---
title: Git
description: 
published: true
date: 2024-10-08T12:28:23.270Z
tags: 
editor: markdown
dateCreated: 2024-03-26T13:42:29.771Z
---

# Git

## Config with multiple personalities (logins)

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

## Find large files in the history

List all objects:
```bash
git verify-pack -v .git/objects/pack/pack*.idx
```

The column represent:
1. object id
1. type
1. size

To find the commit(s) associated with an object id:

```bash
git log --all --find-object=<object id>
```
