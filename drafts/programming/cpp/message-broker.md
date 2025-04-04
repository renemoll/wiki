---
title: Message broker
description: 
published: true
date: 2025-01-11T18:21:00.116Z
tags: 
editor: markdown
dateCreated: 2025-01-11T18:08:54.904Z
---

# Message broker

msg broker
 - send an message to the broker
   - message is a structure
 - broker sends message to all subscribers
   - policy may change behaviour here
     1. Send single message to all subscribers
     2. Send all messages to all subscribers
     3. Send 1 message (may be a different message) to all subscribers

```plantuml
autoactivate on

participant Context
participant Broker
participant Actor

Context -> Broker : run()
  loop for each message as m
    loop for each subscriber of m
      Broker -> Actor: handle_message(msg)
      return
    end
  end
```

```plantuml
autoactivate on

participant Context
participant Broker

== Initialization ==

Context -> Actor1 : initialize()
  Actor1 -> Broker : subscribe(greeting)
  return
return

Context -> Actor2 : initialize()
  Actor2 -> Broker : subscribe(farewell)
  return
return


== Message exchange ==

Context -> Actor3 : execute()
  Actor3 -> Broker : publish(greeting)
  return
return

Context -> Broker : run()
  Broker -> Actor1: handle_message(greeting)
  return
return
```


## Details

* Message encapsulates the actual data structure representing the content (data)
  * The data structure is allocated on a pool
  * The message acts as a reference counter and will release the data to the pool when not in use anymore
  * Messages can only be written opon creation, after that they are read-only
  


## Open questions

* agent registration at compile time?
  * message subscription at compile time?
