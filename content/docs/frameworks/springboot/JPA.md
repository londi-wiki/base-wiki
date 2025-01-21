---
weight: 999
title: "JPA"
description: ""
icon: "article"
date: "2025-01-21T12:00:00+02:00"
lastmod: "2025-01-21T12:00:00+02:00"
draft: false
toc: true
---

# Java Persistence API (JPA) - Einführung

## Was ist JPA?

JPA ist eine Spezifikation für die Verwaltung von Datenbankoperationen in Java-Anwendungen. Es bietet eine objekt-relationalen Mapper (ORM), der Java-Klassen mit Datenbanktabellen verbindet.

**Beispiel**

```Java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;
}
```

**Erklärung**

Diese Klasse repräsentiert eine Tabelle User in der Datenbank. Die Annotationen wie @Entity und @Id sind notwendig, um sie als Datenbankentität zu definieren.

# Entity-Manager und Lebenszyklus

**Funktionsweise**

Verwaltet die Objekte im Persistence Context und führt CRUD-Operationen durch.

**Lebenszyklus von Entitäten**

1. Transient: Das Objekt existiert nur im Speicher
2. Persistent: Das Objekt wird vom Entity Manager verwaltet und mit der Datenbank synchronisiert
3. Detached: Das Objekt ist nicht mehr mit dem Persistence Context verbunden
4. Removed: Das Objekt ist für die Löschung markiert

Beispiel

```Java
EntityManager em = ...;
User user = new User(); // Transient
em.persist(user);       // Persistent
em.detach(user);        // Detached
em.remove(user);        // Removed
```

# Beziehungen zwischen Entitäten

**Definition**

- @OneToOne
- @OneToMany
- @ManyToOne
- @ManyToMany

**FetchType**

- Lazy
- Eager

**Beispiel**

```Java
@Entity
public class User {
    @Id
    private Long id;

    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
    private List<Rental> rentals;
}

@Entity
public class Rental {
    @Id
    private Long id;

    @ManyToOne
    private User user;
}
```

**Erklärung**

Ein User hat viele Rental-Einträge, aber jeder Rental gehört zu genau einem User.


# Vererbung in JPA

**Strategien für Vererbung**

`@Inheritance` definiert, wie die Vererbung auf Datenbankebene abgebildet wird.

**Strategie**

1. SINGLE_TABLE: Eine Tabelle für die gesamte Hierarchie
2. TABLE_PER_CLASS: Eine Tabelle pro konkreter Klasse
3. JOINED: Eine Tabelle für jede Klasse, mit Fremdschlüsseln für die Verbindung

**Beispiel**

```Java
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "dtype", discriminatorType = DiscriminatorType.STRING)
public class Vehicle {
    @Id private Long id;
    private String name;
}

@Entity
@DiscriminatorValue("Car")
public class Car extends Vehicle {
    private int numberOfDoors;
}
```

**Erklärung**

In einer einzigen Tabelle Vehicle werden Autos (dtype = "Car") und andere Fahrzeuge gespeichert.

# JPQL

**Allgemein**

JPQL (Jakarta Persistence Query Language) ist eine SQL-ähnliche Sprache, die auf Entitäten basiert.

**Beispiel**

```Java
TypedQuery<User> query = em.createQuery(
    "SELECT u FROM User u WHERE u.name = :name", User.class);
query.setParameter("name", "Alice");
List<User> users = query.getResultList();
```

**Erklärung**

Die Abfrage ruft alle Benutzer mit dem Namen Alice aus der Datenbank ab.

**Funktionen in JPQL:**

- Aggregate: COUNT, MAX, MIN, AVG.
- Bedingungen: WHERE, LIKE, IN, IS NULL.

# Spring Data JPA

**Grundlagen**

Spring Data JPA generiert automatisch Implementierungen für CRUD-Operationen basierend auf Repository-Interfaces.

**Beispiel**

```Java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByName(String name);
}
```

**Erklärung**

Die Methode findByName wird automatisch implementiert und sucht Benutzer nach Namen.

**DSL-Schlüsselwörter**

- And/Or: findByNameAndEmail.
- Between: findByAgeBetween.
- Like: findByNameLike.


# DTO

**Grundlagen**

Ein DTO ist eine schlanke Datenstruktur, die nur die notwendigen Daten enthält, um Informationen zwischen Schichten zu übertragen.

```Java
public record UserDto(Long id, String name, String email) {}

// ...

User user = userRepo.findById(1L).get();
UserDto dto = new UserDto(user.getId(), user.getName(), user.getEmail());
```
