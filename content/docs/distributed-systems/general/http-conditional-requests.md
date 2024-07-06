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


## Vollständiges Beispiel

Server

```java
import jakarta.inject.Singleton;
import jakarta.ws.rs.*;
import jakarta.ws.rs.core.*;
import org.glassfish.jersey.jdkhttp.JdkHttpServerFactory;
import org.glassfish.jersey.server.ResourceConfig;

import java.net.URI;
import java.net.URISyntaxException;

public class LeonServer {

    public static void main(String[] args) throws URISyntaxException {
        URI baseUri = new URI("http://localhost:2222/");
        ResourceConfig rc = new ResourceConfig(LeonResource.class);
        JdkHttpServerFactory.createHttpServer(baseUri, rc);
        System.out.println("Server started");
    }

    @Singleton
    @Path("/quote")
    public static class LeonResource {

        private static String quote = "Bananen sind gelb.";

        @GET
        @Produces("text/plain")
        public Response get(@Context Request request){
            System.out.println("GET called");
            EntityTag etag = new EntityTag("" + quote.hashCode());
            Response.ResponseBuilder builder = request.evaluatePreconditions(etag);
            if (builder != null) {
                return builder.build();
            }

            return Response.ok(quote, MediaType.TEXT_PLAIN)
                    .tag(new EntityTag("" + quote.hashCode())).build();
        }

        @PUT
        @Consumes("text/plain")
        public Response setTextPlain(String msg) {
            System.out.println("PUT called");
            quote = msg;
            return Response.noContent().build();
        }

    }

}
```

Client

```java
import jakarta.ws.rs.client.Client;
import jakarta.ws.rs.client.ClientBuilder;
import jakarta.ws.rs.client.WebTarget;
import jakarta.ws.rs.core.EntityTag;
import jakarta.ws.rs.core.MediaType;
import jakarta.ws.rs.core.Response;

public class LeonClient {

    public static void main(String[] args) {
        Client c = ClientBuilder.newClient();
        WebTarget r = c.target("http://localhost:2222/quote");

        Response resp1 = r.request().accept(MediaType.TEXT_PLAIN).get();
        EntityTag etag = resp1.getEntityTag();
        System.out.println("etag: " + etag);
        System.out.println("Quote: " + resp1.readEntity(String.class));
        while (true) {
            Response resp2 = r.request().accept(MediaType.TEXT_PLAIN)
                    .header("If-None-Match", etag)
                    .get();

            System.out.println("etag: " + etag);

            if (resp2.getStatus() == Response.Status.NOT_MODIFIED.getStatusCode()) {
                System.out.println("NOT MODIFIED, quote still the same");
            } else {
                System.out.println(">> MODIFIED");
                etag = resp2.getEntityTag();
                System.out.println("new etag: " + etag);
                System.out.println("Quote: " + resp2.readEntity(String.class));
            }

            // Sleep 1 second
            try {
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        }

    }

}
```