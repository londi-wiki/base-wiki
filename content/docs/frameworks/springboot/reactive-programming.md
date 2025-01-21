---
weight: 999
title: "Reactive Programming"
description: ""
icon: "article"
date: "2025-01-21T12:10:00+02:00"
lastmod: "2025-01-21T12:10:00+02:00"
draft: false
toc: false
---

# Reactive Programming

## Allgemein

**Was sind Reactive Systems?**

- Anwendungen, die auf asynchroner Datenverarbeitung und Ressourcenverfügbarkeit reagieren.
- Im Vergleich zu synchronen Systemen bieten reaktive Systeme eine effizientere Ressourcennutzung, da sie Threads nicht blockieren.

**Anwendungsfälle**

- Anwendungen mit vielen gleichzeitigen Verbindungen (z. B. mobile Geräte).
- Datenstreaming und serverseitige Ereignisübermittlung.

# Reactive Streams

**Kernkomponenten**

1. Publisher: Liefert Daten asynchron
2. Subscriber: Abonniert Daten und reagiert auf eingehende Elemente
3. Subscription: Kontrolliert die Datenflüsse zwischen Publisher und Subscriber
4. Processor: Kombiniert die Rollen von Publisher und Subscriber zur Datenverarbeitung

**Backpressure**

Mechanismus, mit dem Verbraucher (Subscriber) die Menge an Daten stuern, die sie verarbeiten können. Dies verhindert Überlastung durch zu schnelle Datenproduktion.

**Beispiel**

```Java
Flux.just("A", "B", "C")
    .map(String::toLowerCase)
    .subscribe(System.out::println);
```

# Project Reactor

- Flux: Stellt 0 bis N Elemente bereit
- Mono: Liefert 0 oder 1 Element

**Beispiel**

```Java
Mono.just("Hallo, Welt!")
    .subscribe(System.out::println);

Flux.just("Eins", "Zwei", "Drei")
    .map(String::toUpperCase)
    .subscribe(System.out::println);
```

# R2DBC (Reactive Database Access)

Unterschied zu JDBC

- R2DBC ermöglicht nicht-blockierende Datenbankzugriffe
- Unterstützung für relationale Datenbanken wie PostgreSQL, MySQL, ...

**Beispiel**

```Java
@Table("PERSONS")
public record Person(
    @Id Long id,
    @Column("name") String name,
    int age
) {}


// Repository Beispiel
interface PersonRepository extends ReactiveCrudRepository<Person, Long> {
    Flux<Person> findByName(String name);
}
```

# Spring WebFlux

**Was ist WebFlux?**

- Eine reaktive Alternative zu Spring MVC, optimiert für non-blocking APIs.
- Unterstützt durch Frameworks wie Netty für asynchrone Netzwerkoperationen.

**Unterschied zwischen Spring MVC und WebFlux**

- MVC verwendet blockierende Aufrufe, während WebFlux asynchrone Flux- und Mono-Datenströme nutzt.

```Java
@RestController
public class ExampleController {
    @GetMapping("/stream")
    public Flux<String> stream() {
        return Flux.interval(Duration.ofSeconds(1))
                   .map(String::valueOf);
    }
}
```

# WebFlux WebClient

- Alternative zu RestTemplate
- Ermöglicht asynchrone HTTP-Anfragen mit Flux- und Mono-Unterstützung.

```Java
WebClient client = WebClient.create("http://localhost:8080");
client.get().uri("/stream")
      .retrieve()
      .bodyToFlux(String.class)
      .subscribe(System.out::println);
```

# WebSockets mit WebFlux

- Ermöglicht bidirektionale Kommunikation zwischen Client und Server.
- WebSocketHandler wird für die Verwaltung von WebSocket-Sitzungen genutzt.

**Beispiel**

```Java
@Service
public class MyWebSocketHandler implements WebSocketHandler {
    @Override
    public Mono<Void> handle(WebSocketSession session) {
        return session.send(session.receive()
            .map(WebSocketMessage::getPayloadAsText)
            .map(String::toUpperCase)
            .map(session::textMessage));
    }
}
```

**RSocket**

- Protokoll für reaktive Kommunikation:
- Unterstützt bidirektionale Kommunikation und Backpressure.
- Geeignet für Microservices und Echtzeitanwendungen.

```Java
@Controller
public class RSocketController {
    @MessageMapping("channel")
    public Flux<String> processChannel(Flux<String> input) {
        return input.map(String::toUpperCase);
    }
}
```
