---
weight: 999
title: "Http Conditional Requests"
description: ""
icon: "article"
date: "2024-03-25T09:32:50+01:00"
lastmod: "2024-03-25T09:32:50+01:00"
draft: false
toc: true
---

## Allgemein

Mit `ResponseBuilder builder = request.evaluatePreconditions(etag);` kann man sicherstellen, dass auf die Precondition geprüft wird.
Dies kann beim Client mit dem Header `If-Match` und `If-None-Match` gemacht werden.

## Beispiel

```java
@GET
@Path("/value")
@Produces("text/plain")
public Response getValue(@Context Request request) {
    EntityTag etag = new EntityTag("123");
    ResponseBuilder builder = request.evaluatePreconditions(etag);
    if (builder != null) {
        return builder.build();
    } else {
        return Response.ok("42", MediaType.TEXT_PLAIN)
                .tag(new EntityTag("123"))
                .build();
    }
}

// ...

public static void main(String[] args) {
    Client c = ClientBuilder.newClient();
    WebTarget r = c.target("http://localhost:9999/test/");
    Response resp = r.path("value")
            .request("text/plain")
            .header("If-None-Match", "\"123\"")
            .get();
    System.out.println(resp.getStatus());
}
```

Liest man so: "get if none match '123'" und würde in diesem Fall Status **304** zurückgeben.

Würde Folgendes stehen:

```java
public static void main(String[] args) {
    Client c = ClientBuilder.newClient();
    WebTarget r = c.target("http://localhost:9999/test/");
    Response resp = r.path("value")
            .request("text/plain")
            .header("If-Match", "\"123\"")
            .get();
    System.out.println(resp.getStatus());
}
```

Liest man so: "get if match '123'" und würde in diesem Fall Status **200** zurückgeben.
