---
weight: 999
title: "Reactivestreams"
description: ""
icon: "article"
date: "2024-12-03T10:22:35+01:00"
lastmod: "2024-12-03T10:22:35+01:00"
draft: false
toc: true
---

# Mono und flux

## Mono

```java
public static void main(String[] args) {
    Mono<String> m = Mono.just("Hello World");

    m.subscribe(System.out::println);
    m.subscribe(s -> System.out.println(s));

    m.subscribe(new Subscriber<>() {
        @Override
        public void onSubscribe(Subscription s) {
            System.out.println("onSubscribe");
            s.request(3);
        }

        @Override
        public void onNext(String t) {
            // wird erst aufgeführt wenn wenn auf der Subscription requested wird. "s.request(...)"
            System.out.println("onNext " + t);
        }

        @Override
        public void onError(Throwable t) {
            System.out.println(t);
        }

        @Override
        public void onComplete() {
            // wird erst aufgeführt wenn wenn auf der Subscription requested wird. "s.request(...)"
            System.out.println("onComplete");
        }
    });
}
```

## Flux

```java
public static void main(String[] args) {
    Flux.just("one", "two", "three", "four")
        .log()
        .map(String::toUpperCase)
        .log()
        .subscribe();
}

/*
10:29:07.677 [main] INFO reactor.Flux.Array.1 -- | onSubscribe([Synchronous Fuseable] FluxArray.ArraySubscription)
10:29:07.681 [main] INFO reactor.Flux.MapFuseable.2 -- | onSubscribe([Fuseable] FluxMapFuseable.MapFuseableSubscriber)
10:29:07.682 [main] INFO reactor.Flux.MapFuseable.2 -- | request(unbounded)
10:29:07.682 [main] INFO reactor.Flux.Array.1 -- | request(unbounded)
10:29:07.682 [main] INFO reactor.Flux.Array.1 -- | onNext(one)
10:29:07.682 [main] INFO reactor.Flux.MapFuseable.2 -- | onNext(ONE)
10:29:07.682 [main] INFO reactor.Flux.Array.1 -- | onNext(two)
10:29:07.682 [main] INFO reactor.Flux.MapFuseable.2 -- | onNext(TWO)
10:29:07.682 [main] INFO reactor.Flux.Array.1 -- | onNext(three)
10:29:07.682 [main] INFO reactor.Flux.MapFuseable.2 -- | onNext(THREE)
10:29:07.682 [main] INFO reactor.Flux.Array.1 -- | onNext(four)
10:29:07.682 [main] INFO reactor.Flux.MapFuseable.2 -- | onNext(FOUR)
10:29:07.683 [main] INFO reactor.Flux.Array.1 -- | onComplete()
10:29:07.683 [main] INFO reactor.Flux.MapFuseable.2 -- | onComplete()
*/
```

## Unterschiede zwischen Mono und Flux

### Mono

**Definition:** Ein Mono repräsentiert 0 oder **1 Element** in einem asynchronen Stream.
**Einsatzbereich:** Wird verwendet, wenn du sicher bist, dass es entweder ein einzelnes Ergebnis gibt oder keins (z. B. Datenbankabfragen, 
die ein einzelnes Objekt zurückgeben könnten, oder ein API-Call).

Beispiel:
```java
Mono<String> mono = Mono.just("Hello, Mono!");
// oder:
Mono<String> emptyMono = Mono.empty();
// oder:
Mono<Void> ... // Z.B. um zu Signalisieren, dass ein Prozessschritt vollständig abgeschlossen wurde. 
```

### Flux

**Definition:** Ein Flux repräsentiert 0 bis **n Elemente** in einem asynchronen Stream.
**Einsatzbereich:** Wird verwendet, wenn du mehrere Elemente erwartest, z. B. eine Liste von Datenbankeinträgen oder kontinuierlich eintreffende Daten wie Websocket-Nachrichten.

Beispiel:
```java
Flux<String> flux = Flux.just("Hello", "Flux", "World!");
//oder:
Flux<String> emptyFlux = Flux.empty();
```