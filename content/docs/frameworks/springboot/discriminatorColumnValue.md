---
weight: 999
title: "DiscriminatorColumnValue"
description: ""
icon: "article"
date: "2024-09-24T18:50:15+02:00"
lastmod: "2024-09-24T18:50:15+02:00"
draft: false
toc: true
---

## Discriminator column und value

Mit dieser Annotation kann bei der Implementierungen mehreren Varianten einer (abstrakten) Klasse die gleiche Tabelle verwendet werden.
Für die Unterscheidung kann dann eine separate Spalte "Type" verwendet werden.

## Beispiel

**PriceCategory**

```java
@Entity
@Table(name = "PRICECATEGORIES")
@DiscriminatorColumn(discriminatorType = DiscriminatorType.STRING, name = "PRICECATEGORY_TYPE")
@JsonDeserialize(using = PriceCategoryDeserializer.class)
@JsonSerialize(using = PriceCategorySerializer.class)
public abstract class PriceCategory {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "PRICECATEGORY_ID")
    private Long id;

    public PriceCategory(){}

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public abstract double getCharge(int daysRented);

    public int getFrequentRenterPoints(int daysRented) {
        return 1;
    }
}
```

**PriceCategoryRegular**

```java
@Entity
@DiscriminatorValue("Regular")
public class PriceCategoryRegular extends PriceCategory {

    @Override
    public double getCharge(int daysRented) {
        double result = 2;
        if (daysRented > 2)
            result += (daysRented - 2) * 1.5;
        return result;
    }

    @Override
    public String toString() {
        return "Regular";
    }
}
```

### Datenbank Modell

**Schema**

```sql
CREATE TABLE PRICECATEGORIES
(
    PRICECATEGORY_ID   BIGINT AUTO_INCREMENT PRIMARY KEY,
    PRICECATEGORY_TYPE VARCHAR(31) NOT NULL
);
```

**Inhalt**

```sql
INSERT INTO PRICECATEGORIES (PRICECATEGORY_TYPE) VALUES ('Regular');
INSERT INTO PRICECATEGORIES (PRICECATEGORY_TYPE) VALUES ('Children');
INSERT INTO PRICECATEGORIES (PRICECATEGORY_TYPE) VALUES ('NewRelease');
```
