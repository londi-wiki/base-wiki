---
weight: 999
title: "Design Pattern Examples"
description: ""
icon: "article"
date: "2025-01-22T00:30:00+02:00"
lastmod: "2025-01-22T00:30:00+02:00"
draft: false
toc: true
---

# Design Pattern Examples

## Aufgaben - Pattern herausfinden

**Beschreibung 1**

Es gibt eine Familie von Algorithmen, und die Implementierung kann je nach Situation dynamisch gewechselt werden, ohne die eigentliche Klasse zu ändern.

**Beschreibung 2**

Ein Objekt dient als zentraler Zugangspunkt für die Erstellung verschiedener miteinander verwandter Objekte, ohne dass der konkrete Typ der Objekte bekannt ist.

**Beschreibung 3**

Beobachter-Objekte registrieren sich bei einem Subjekt, um benachrichtigt zu werden, wenn sich dessen Zustand ändert.

**Beschreibung 4**

Ein Objekt stellt sicher, dass nur eine einzige Instanz davon existiert, und bietet einen globalen Zugriffspunkt.

**Beschreibung 5**

Ein komplexes Objekt wird schrittweise erstellt, wobei jede Stufe durch eine separate Klasse definiert ist. Ein „Direktor“ koordiniert den Bauprozess.


## Aufgaben - Pattern umsetzen

**Singleton Pattern**

Beschreibe, was dieses Pattern macht und erstelle ein Beispiel, das eine Logger-Klasse implementiert, die in einem System nur eine Instanz haben darf.

**Factory Pattern**

Erkläre, wie dieses Pattern funktioniert, und implementiere ein Beispiel für die Erstellung von verschiedenen Pizza-Typen (z. B. Margherita, Salami, Veggie).

**Observer Pattern**

Beschreibe, wie das Observer Pattern arbeitet, und zeige ein Beispiel einer Wetterstation, bei der sich mehrere Wetteranzeigen registrieren.

**Strategy Pattern**

Beschreibe die Funktionsweise und erstelle ein Beispiel, bei dem eine Zahlungsstrategie (z. B. Kreditkarte oder PayPal) gewählt wird.

**Decorator Pattern**

Beschreibe die Idee hinter diesem Pattern und erstelle ein Beispiel, bei dem die Grundfunktionalität einer Pizza durch Toppings wie Käse und Salami erweitert wird.

## Lösungen - Pattern herausfinden

**Singleton Pattern**

Beschreibe, was dieses Pattern macht und erstelle ein Beispiel, das eine Logger-Klasse implementiert, die in einem System nur eine Instanz haben darf.

**Factory Pattern**

Erkläre, wie dieses Pattern funktioniert, und implementiere ein Beispiel für die Erstellung von verschiedenen Pizza-Typen (z. B. Margherita, Salami, Veggie).

**Observer Pattern**

Beschreibe, wie das Observer Pattern arbeitet, und zeige ein Beispiel einer Wetterstation, bei der sich mehrere Wetteranzeigen registrieren.

**Strategy Pattern**

Beschreibe die Funktionsweise und erstelle ein Beispiel, bei dem eine Zahlungsstrategie (z. B. Kreditkarte oder PayPal) gewählt wird.

**Decorator Pattern**

Beschreibe die Idee hinter diesem Pattern und erstelle ein Beispiel, bei dem die Grundfunktionalität einer Pizza durch Toppings wie Käse und Salami erweitert wird.

## Lösungen - Pattern umsetzen

**Singleton Pattern - Logger**

```Java
class Logger {
    private static Logger instance

    private Logger() { } // Verhindert direkte Instanziierung

    static Logger getInstance() {
        if (instance == null) {
            instance = new Logger()
        }
        return instance
    }

    void log(String message) {
        print("Log: " + message)
    }
}

// Beispielnutzung
Logger logger = Logger.getInstance()
logger.log("Dies ist ein Singleton-Logger.")

```

**Factory Pattern - Pizza-Fabrik**

```Java
abstract class Pizza {
    abstract void backen()
}

class Margherita : Pizza {
    void backen() {
        print("Backe eine Margherita-Pizza.")
    }
}

class Salami : Pizza {
    void backen() {
        print("Backe eine Salami-Pizza.")
    }
}

class PizzaFabrik {
    Pizza erstellen(String typ) {
        if (typ == "Margherita") return new Margherita()
        if (typ == "Salami") return new Salami()
        return null
    }
}

// Beispielnutzung
PizzaFabrik fabrik = new PizzaFabrik()
Pizza pizza = fabrik.erstellen("Salami")
pizza.backen()

```

**Observer Pattern - Wetterstation**

```Java
interface Beobachter {
    void aktualisieren(double temperatur)
}

class Wetteranzeige : Beobachter {
    String name
    Wetteranzeige(String name) { this.name = name }

    void aktualisieren(double temperatur) {
        print(name + " zeigt neue Temperatur: " + temperatur + "°C")
    }
}

class Wetterstation {
    List<Beobachter> beobachterListe = []
    double temperatur

    void anmelden(Beobachter o) { beobachterListe.add(o) }
    void abmelden(Beobachter o) { beobachterListe.remove(o) }

    void setTemperatur(double temperatur) {
        this.temperatur = temperatur
        for (Beobachter o : beobachterListe) { o.aktualisieren(temperatur) }
    }
}

// Beispielnutzung
Wetterstation station = new Wetterstation()
station.anmelden(new Wetteranzeige("Anzeige 1"))
station.setTemperatur(22.0)

```

**Strategy Pattern - Zahlungsstrategien**

```Java
interface Zahlungsstrategie {
    void zahlen(double betrag)
}

class Kreditkarte : Zahlungsstrategie {
    void zahlen(double betrag) { print("Zahle " + betrag + " mit Kreditkarte.") }
}

class PayPal : Zahlungsstrategie {
    void zahlen(double betrag) { print("Zahle " + betrag + " mit PayPal.") }
}

class BezahlContext {
    Zahlungsstrategie strategie
    void setStrategie(Zahlungsstrategie strategie) { this.strategie = strategie }
    void ausfuehrenZahlung(double betrag) { strategie.zahlen(betrag) }
}

// Beispielnutzung
BezahlContext context = new BezahlContext()
context.setStrategie(new Kreditkarte())
context.ausfuehrenZahlung(100.0)

```

**Decorator Pattern - Pizza-Toppings**

```Java
abstract class Pizza {
    abstract String beschreibung()
    abstract double preis()
}

class BasisPizza : Pizza {
    String beschreibung() { return "Basis Pizza" }
    double preis() { return 5.0 }
}

abstract class PizzaDecorator : Pizza {
    Pizza pizza
    PizzaDecorator(Pizza pizza) { this.pizza = pizza }
}

class Kaese : PizzaDecorator {
    Kaese(Pizza pizza) : super(pizza) {}
    String beschreibung() { return pizza.beschreibung() + ", Käse" }
    double preis() { return pizza.preis() + 1.5 }
}

class Salami : PizzaDecorator {
    Salami(Pizza pizza) : super(pizza) {}
    String beschreibung() { return pizza.beschreibung() + ", Salami" }
    double preis() { return pizza.preis() + 2.0 }
}

// Beispielnutzung
Pizza pizza = new BasisPizza()
pizza = new Kaese(pizza)
pizza = new Salami(pizza)
print(pizza.beschreibung() + " kostet " + pizza.preis() + "€")

```
