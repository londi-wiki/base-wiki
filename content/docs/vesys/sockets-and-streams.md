---
weight: 999
title: "Sockets and streams"
description: ""
icon: "article"
date: "2024-02-19T08:25:14+01:00"
lastmod: "2024-02-19T08:25:14+01:00"
draft: false
toc: true
---

# Sockets

## Simple echo server

```java
try (ServerSocket ss = new ServerSocket(1234);
     Socket s = ss.accept();
     InputStream in = s.getInputStream();
     OutputStream out = s.getOutputStream()
) {
    in.transferTo(out);
} catch (IOException e) {
    throw new RuntimeException(e);
}
```

try out:

```bash
> telnet localhost 1234
> hello
hello
```
