---
weight: 999
title: "PersistenceContext"
description: ""
icon: "article"
date: "2024-09-23T14:24:37+02:00"
lastmod: "2024-09-23T14:24:37+02:00"
draft: false
toc: true
---

# DAO Pattern

**Data Access Object Pattern (Repository Pattern)**: Strategy Pattern

- Jeder Datenbank Zugriff wird über das DOA (Repository) realisiert
- Jede DAO Instanz is für jeweils ein Domain Objekt verantwortlich
- CRUD
- DAO ist **nicht** für das Verwalten (handling) von Transaktionen, Session oder Verbindungen zuständig

Beispiel:

```java
public interface Repository<T, ID extends Serializable> {
   Optional<T> findById(ID id); 
   List<T>     findAll();

   T           save(T t);

   void        deleteById(ID id); 
   void        delete(T entity);

   boolean     existsById(ID id); 
   long        count();
}
```

# Entity Manager

- Stell folgende Funktionen zur Verfügung:
  - find
  - persist
  - update
  - remove
- Persistence context & controlled lifecycle

**Entität**

```java
@Entity
public class Movie {
    @Id
    @GeneratedValue
    private Long id;
    ...
}
```

**Entity Manager**

```java
@Service
@Transactional // Führt die Transaktion automatisch am Ende der Funktion aus (falls nicht schon geschehen)
public class MovieService {

   @PersistenceContext 
   private EntityManager em;

   public Long saveNewMovie(String title, LocalDate date) {
      Movie m = new Movie(title, date); 
      em.persist(m);
      return m.getId();
   }

   public void rentMovie(Long id) {
      Movie m = em.find(Movie.class, id);
      m.setRented(true); // will be persisted at the end of the TX 
   }
}
```

## Annotations

### @Entity

- Parameterlosen public oder protected Konstruktor
- Klasse darf nicht final sein
- Persistent Instanz-Felder dürfen nicht final sein
- Top Level Klasse
  - keine nicht-statische innere Klasse
  - kein interface
  - kein enum
  - kein record

