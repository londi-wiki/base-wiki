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

Eigenschaften:
- Stell folgende Funktionen zur Verfügung:
  - find
  - persist
  - update
  - remove
- Persistence context & controlled lifecycle

Aufgaben:
- Speichert Entitäten in einem Persistence Context (PC)
- Managed den Lifecycle einer Entität Instanz
  - Eine Instanz im PC is "attached"
  - Eine nicht assoziierte Instanz is unmanaged (detached)

Persistenzkontext = Menge der verwalteten Objekte
- Es darf nur eine Entitätsinstanz mit derselben persistenten Identität in einem
  Persistenzkontext existieren
- Entity Manager synchronisiert automatisch den Inhalt des PC mit der Datenbank
- Änderungen, die an verwalteten Objekten vorgenommen werden, werden automatisch angewendet (flushed)

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

```java
@Target(TYPE) @Retention(RUNTIME) 
public @interface Entity {
   String name() default "";
}
```

- Parameterlosen public oder protected Konstruktor
- Klasse darf nicht final sein
- Persistent Instanz-Felder dürfen nicht final sein
- Top Level Klasse
  - keine nicht-statische innere Klasse
  - kein interface
  - kein enum
  - kein record

### @Table

"Datenbank name"

```java
@Target(TYPE) @Retention(RUNTIME) 
public @interface Table {
   String name() default "";
   String catalog() default "";
   String schema() default "";
   UniqueConstraint[] uniqueConstaints() default {};
}
```

– name name of the table unqualified name of the entity class or name of the @Entity annotation!
– catalog catalog of the table standard catalog
– schema schema of the table standard schema
– uniqueConstraints constraints applied to generated DDL tables

**Beispiel**

```java
@Table(name = "DEMO_USER", uniqueConstraints = { 
   @UniqueConstraint(columnNames = { "PHONENR", "AREA-CODE" })
})
```

### @Column

"Spezifiziert die abgebildete Spalte für das persistente Property"

```java
@Target({METHOD, FIELD}) @Retention(RUNTIME) 
public @interface Column {
    String name() default ""; // name of column
    boolean unique() default false; // if DB column is unique 
    boolean nullable() default true; // if DB column is nullable 
    boolean insertable() default true; // if manipulation with a
    // sql insert is allowed
    boolean updatable() default true;
    String columnDefinition() default ""; // e.g. CLOB / BLOB 
    String table() default ""; // table in which field 
    // is stored (sec. table)
    int length() default 255; // size for strings 
    int precision() default 0; // decimal precision 
    int scale() default 0; // decimal scale
}
```

### @Enumerated

"Spezifiziert das Abbilden von Enumerationen"

```java
@Target({METHOD,FIELD}) @Retention(RUNTIME) 
public @interface Enumerated {
   EnumType value() default ORDINAL;
}
```

Value field:
- EnumType.ORDINAL
- Value is stored as an integer
- EnumType.STRING
- Value is stored as a string

### @Id

"Spezifiziert Primary Key"

```java
@Target({METHOD,FIELD}) @Retention(RUNTIME)
public @interface Id {
}
```

Possible types for primary keys:
- Primitive types: byte, int, short, long, char
- Wrapper types: Byte, Integer, Short, Long, Character
- Arrays of primitives or wrappers
- Strings: java.lang.String
- Large numerics: java.math.BigInteger
- Temporal types: java.util.Date, java.sql.Date, java
- UUID: java.util.UUID (since JPA 3.1)

#### Primary Keys Generierung**

**Assigned**

Primary keys may be assigned by the application, i.e. no key generation
is necessary
- E.g. language table: primary key is the ISO country code
- Assigned UUID (global unique identifier) in the application

**Identity**
– Auto increment supported by some DBs

**Sequence**
– Some DBs support sequences which generate unique values

**Table**
– Primary keys are stored in a separate PK table

**UUID**
– Primary keys are universally unique identifiers (RFC 4122)

### @GeneratedValue

"Spezifiziert Primary Key Generierung"

```java
@Target({METHOD,FIELD}) @Retention(RUNTIME)
public @interface GeneratedValue {
    GenerationType strategy() default AUTO;
    String generator() default "";
}

public enum GenerationType { TABLE, SEQUENCE, IDENTITY, UUID, AUTO };
```

– strategy primary key generation strategy
    - UUID was added with JPA 3.1
– generator name of the generator as specified or TableGenerator annotations

## Assozationen

– @OneToOne
– @OneToMany
– @ManyToOne
– @ManyToMany

### ManyToOne

**Rental**
```java
@Entity
public class Rental {
   @Id @GeneratedValue 
   private int id;

 @ManyToOne // Rental is the owner of the relationship 
   @JoinColumn(name = "USER_FK") // optional
   private User user;

   public Rental() { }

   public User getUser() { return user; }
   public void setUser (User user) { this.user = user; }

   public int getId() { return id; }
   public void setId(int id) { this.id = id; }
}
```

**User**
```java
@Entity
public class User {
   ...
   @OneToMany(mappedBy = "user") 
   private List<Rental> rentals;
 // this is the inverse side of the relationship

   public Collection<Rental> getRentals() {
      return rentals;
   }
   public void setRentals(Collection<Rental> rentals) {
      this.rentals = rentals; 
   }
}
```

