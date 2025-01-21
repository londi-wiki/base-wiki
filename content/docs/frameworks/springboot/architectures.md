---
weight: 999
title: "Architectures"
description: ""
icon: "article"
date: "2025-01-22T00:00:00+02:00"
lastmod: "2025-01-22T00:00:00+02:00"
draft: false
toc: true
---

# Architectures

## Arten

### Monolith

**Eigenschaften**

- Alle Komponenten in einer einzigen Einheit gebündelt.
- Enge Kopplung der Module.
- Zentrale Datenhaltung.

**Vorteile**

- Einfaches Deployment und geringe Infrastrukturkomplexität.

**Nachteile**

- Schwer skalierbar, eingeschränkte Modularität.


### Modulith

**Definition**

- Eine modulare Struktur innerhalb eines Monolithen.

**Eigenschaften**

- Module sind logisch und funktional getrennt, teilen sich jedoch denselben Deployment-Prozess.
- Klare Schnittstellen für die interne Kommunikation.

**Vorteile**

- Bessere Wartbarkeit und Erweiterbarkeit.
- Kombination der Einfachheit eines Monolithen mit der Modularität von Microservices.

### Microservices

**Definition**

- Eigenständige Dienste, die spezifische Funktionalitäten abdecken und unabhängig voneinander entwickelt, bereitgestellt und skaliert werden können.

**Vorteile**

- Hohe Flexibilität und Skalierbarkeit.
- Technologische Vielfalt.

**Nachteile**

- Komplexe Kommunikation und Infrastruktur.

# Modulith und eventbasierte Kommunikation

**Vorteile**

- Lose Kopplung zwischen Modulen.
- Bessere Testbarkeit und Flexibilität.
- Asynchrone Verarbeitung und Skalierbarkeit.

## Spring ApplicationEventPublisher

Ermöglicht das Veröffentlichen von Ereignissen in einer Spring-Anwendung.

```Java
@Service
public class CustomerManagement {
    private final ApplicationEventPublisher eventPublisher;

    @Transactional
    public Customer createCustomer(Customer customer) {
        Customer savedCustomer = customerRepository.save(customer);
        eventPublisher.publishEvent(new CustomerCreatedEvent(savedCustomer.getId()));
        return savedCustomer;
    }
}
```

## Listener für Ereignisse

Nutzung von @ApplicationModuleListener für modulare Listener.

```Java
@Service
public class ReservationManagement {
    @ApplicationModuleListener
    @Transactional
    void on(CustomerCreatedEvent event) {
        // Verarbeitung des Ereignisses
    }
}
```

# Eventbasierte Microservices mit RabbitMQ

**Allgemein**

RabbitMQ wird verwendet, um Nachrichten zwischen Microservices asynchron zu verarbeiten.

**RabbitMQ Konfiguration**

```Java
@Service
public class ReservationManagement {
    @RabbitListener(queues = {"customer-queue"})
    public void receiveMessage(Message message) {
        // Nachricht verarbeiten
    }
}
```

**Broker-Konfiguration**

```Java
@Configuration
class LibraryAmqpConfiguration {
    public static final String CUSTOMER_QUEUE = "customer-queue";

    @Bean
    Queue queueCustomer() {
        return new Queue(CUSTOMER_QUEUE, true);
    }
}
```

# Migration von Monolith zu Modulith

**Ziele**

- Modularisierung der Anwendung mit klar definierten Modulen.
- Nutzung von Spring Data JDBC für einfachere Datenzugriffe.
- Vereinfachung der Infrastruktur durch gemeinsame Datenbankhaltung.

**Beispiel-Migration**

- RESTful APIs für jedes Modul bereitstellen.
- Module wie Customer, Book und Reservation trennen, aber im selben Deployment halten.
