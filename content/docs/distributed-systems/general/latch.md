---
weight: 999
title: "Latch"
description: ""
icon: "article"
date: "2024-04-20T22:54:27+02:00"
lastmod: "2024-04-20T22:54:27+02:00"
draft: false
toc: true
---

## CountDownLatch

```java
public static CountDownLatch latch = new CountDownLatch(1);

// ...

// wait for releasing
latch.await();

// ...
        
        
// release on "step"
latch.countDown();
```

---

## Siehe auch

- → [Networking in Java](/docs/distributed-systems/general/networking) – Sockets, InetAddress und Netzwerkschnittstellen
- → [Funktionale Programmierung in Java](/docs/programming-languages/java/functional-programming) – Lambdas, Functional Interfaces, Streams und Optional
