---
weight: 999
title: "Rabbitmq"
description: ""
icon: "article"
date: "2024-07-06T16:37:15+02:00"
lastmod: "2024-07-06T16:37:15+02:00"
draft: false
toc: true
---

# Overview

- Publisher publishes to Exchange
- Exchange routes to queue(s)
- consumer consumes from a queue

Publisher can send a message to one or multiple exchanges.
Between Exchanges and queues are bindings that are controlling the flow:
- direct exchange: Direct redirect message to queue (1:1 or 1:n if multiple queues are used) with the same routing key that is used to publish a message will receive the message.
- fanout exchange: broadcast of the message to all queues that are bound to it
- topic exchange: routes messages to all queues that have a binding key that matches the routing key (regex)
- headers exchange: messages are routed by more sophisticated rules (custom message headers).

## Metadata

- exchanger
- routing key
- payload

A queue can be subscribed by one or multiple consumers leading to the situation that a message is either received by subscriber 1 or 2.
Typically, a queue has often only one subscriber.

