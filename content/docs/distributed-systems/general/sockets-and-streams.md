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

## Quote Server

```java
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;
import java.net.SocketTimeoutException;
import java.util.List;
import java.util.concurrent.CopyOnWriteArrayList;

public class QuoteServer {

    static String quote = "Bananen sind gelb";
    static List<Socket> socketList = new CopyOnWriteArrayList<>(); // threadsafe list implementation
    static int SOCKET_TIMEOUT = 60*1000;

    static BufferedReader toReader(InputStream is) {
        return new BufferedReader(new InputStreamReader(is));
    }

    static PrintWriter toWriter(OutputStream os) {
        return new PrintWriter(os, true);
    }

    public static void main(String[] args) throws IOException {

        int port = 1234;
        try (ServerSocket server = new ServerSocket(port)) {
            System.out.println("Server started.");
            while (true) {
                Socket s = server.accept();
                s.setSoTimeout(SOCKET_TIMEOUT);
                socketList.add(s);
                Thread t = new Thread(() -> {
                    try {
                        while (true) {
                            BufferedReader bf = toReader(s.getInputStream());
                            PrintWriter pr = toWriter(s.getOutputStream());
                            String line = bf.readLine();
                            if (line == null) {
                                socketList.remove(s);
                                break;
                            }
                            if (line.equals("GET")) {
                                pr.println(quote);
                            } else if (!quote.equals(line)) {
                                quote = line;
                                for (Socket fs : socketList) {
                                    toWriter(fs.getOutputStream()).println(quote);
                                }
                            }
                        }
                    } catch (SocketTimeoutException e) {
                        System.err.println("Socket closed");
                    } catch (IOException e) {
                        throw new RuntimeException(e);
                    }
                    System.out.println("Adee: " + s);
                });
                t.start();
            }
        }

    }

}
```
