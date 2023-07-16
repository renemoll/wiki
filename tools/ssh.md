---
title: SSH
description: 
published: true
date: 2023-07-16T13:53:20.237Z
tags: 
editor: markdown
dateCreated: 2023-07-16T13:53:20.237Z
---

# SSH

# Login script

```bash
SSH_ENV="$HOME/ssh/environment"

function start_agent {
    echo "Initializing new SSH agent..."
    touch $SSH_ENV
    chmod 600 "${SSH_ENV}"
    /usr/bin/ssh-agent | sed 's/^echo/#echo/' >> "${SSH_ENV}"
    . "${SSH_ENV}" > /dev/null
    /usr/bin/ssh-add $HOME/ssh/id_rene
}

# Source SSH settings, if applicable
if [ -f "${SSH_ENV}" ]; then
    . "${SSH_ENV}" > /dev/null
    kill -0 $SSH_AGENT_PID 2>/dev/null || {
        start_agent
    }
else
    start_agent
fi
```

