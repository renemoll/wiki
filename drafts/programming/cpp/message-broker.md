---
title: Message broker
description: 
published: true
date: 2025-01-11T18:08:54.904Z
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

Broker : run()
  loop for each message as m
    loop for each subscriber of m
    end
  end


@startuml
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


@enduml