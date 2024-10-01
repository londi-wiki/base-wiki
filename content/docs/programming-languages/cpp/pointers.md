---
weight: 999
title: "Pointers"
description: ""
icon: "article"
date: "2024-10-01T18:31:34+02:00"
lastmod: "2024-10-01T18:31:34+02:00"
draft: false
toc: true
---

# Referenzen

```cpp
int a = 4;
int& b = a;
b = 5;
std::cout << "a: " << a << std::endl; // 5
std::cout << "b: " << b << std::endl; // 5
```


# Rawpointer

```cpp
int x = 5; // x wird direkt mit 5 initialisiert
int* px = &x; // initialisierter Zeiger auf Integer x 
*px = 7; // Wert von x wird indirekt auf 7 gesetzt

Point pnt1; // Punktobjekt auf dem Stack
Person pers1("Anna", 22); // Person auf dem Stack
Point *pnt2 = new Point(); // Punktobjekt auf dem Heap 
Person *pers2 = new Person("Urs", 21); // Person auf dem Heap

pnt1.m_x = 3; // direkter Zugriff auf Instanzvariable m_x
(*pnt2).m_x = 4;// indirekter Zugriff auf Instanzvariable m_x 
pnt2->m_x = 5; // vereinf. Schreibweise des indirekten Zugriffs
```

# Vergleich: Referenzen und Pointer

| Eigenschaft                | Referenzen (&)                            | Pointer (\*)                               |
| -------------------------- |-------------------------------------------|--------------------------------------------|
| Muss initialisiert werden  | **Ja**                                    | Nein                                       |
| Kann nullptr sein          | Nein                                      | Ja                                         |
| Kann neu zugewiesen werden | Nein                                      | Ja                                         |
| Syntax                     | Einfacher, kein Dereferenzierungsoperator | Erfordert Dereferenzierung (\*)            |
| Sicherer                   | Ja, keine nullptr\-Referenz möglich       | Weniger sicher, kann nullptr sein          |
| Speicherverwaltung         | Nicht für dynamischen Speicher geeignet   | Gut für dynamischen Speicher (new, delete) |
| Arithmetik möglich         | Nein                                      | Ja                                         |


# Smart Pointer

Mit Smart pointers benötigt man kein explizites `new` oder `delete`. Letztes wird mit dem Dekonstruktor automatisch ausgeführt.
Smart pointers geben automatisch den Speicherplatz frei, sobald sie nicht mehr verwendet/gebraucht werden. Dazu kommt ein "Reference counter" zum Einsatz.

Es gibt drei Arten von Smart Pointer.
- std::unique_ptr<T>
  - Es existiert pro Objekt höchstens ein einzigartiger Besitzer
  - unique_ptr ist der Besitzer des Objektes, auf welches verwiesen wird
  - wird als Returntyp von Factories verwendet
  - das Objekt wird beim Aufruf des Destruktors des Zeigerobjekts zerstört
  - Heap-Objekt kann mehrere Besitzer haben
- std::shared_ptr<T>
  - mehrere Zeigerobjekte können auf das gleiche Objekt zeigen
  - shared_ptr benutzt **Referenzzähler**
  - das Objekt wird beim Aufruf des Destruktors des Zeigerobjekts nur dann zerstört, wenn keine weiteren shared_ptr aufs gleiche Objekt zeigen
- std::weak_ptr<T>
  - wie shared_ptr, aber ohne Referenzzähler
  - wird zum manuellen Aufbrechen von zyklischen Abhängigkeiten benötigt



```cpp
int main() {
    Person sepp{"Sepp", 33};
    Person susi{"Susi", 44};
    Person & r = sepp;

    std::cout << "--- Referenzen ---" << std::endl;

    std::cout << r << std::endl;
    std::cout << susi << std::endl;
    
    std::cout << "\n--- Smartpointer ---" << std::endl;
    // std::unique_ptr<Person> heidi = std::make_unique<Person>("Heidi", 50); // Type manuell festlegen
    auto hans = std::make_shared<Person>("Hans", 53); // Type automatisch festlegen
    auto heidi = std::make_unique<Person>("Heidi", 50); // Type automatisch festlegen
    // auto petra2 = petra; // Geht nicht
    auto hans2 = hans; // Geht
    std::weak_ptr<Person> wpHans = hans;

    std::cout << *heidi << std::endl;
    std::cout << (*heidi).getName() << std::endl; // Zugriff auf Methode via Dereferenzierung
    std::cout << heidi->getAge() << std::endl; // Zugriff auf Methode via Pfeil

    std::cout << *hans << std::endl;
    std::cout << (*hans).getName() << std::endl; // Zugriff auf Methode via Dereferenzierung
    std::cout << hans->getAge() << std::endl; // Zugriff auf Methode via Pfeil

    std::weak_ptr<Person> wp = hans;
    hans.reset();
    if (wp.expired()) {
        std::cout << "Hans deleted" << std::endl;
    }
    
    std::cout << "\n--- Rawpointer ---" << std::endl;

    Person* petra = new Person("Petra", 30, hans);
    Person* pSepp = &sepp; // Zeigt auf das Objekt sepp

    std::cout << "Pointer Address: " << petra << std::endl; // Pointer adresse
    std::cout << *petra << std::endl; // Dereferenzierung
    std::cout << (*petra).getName() << std::endl; // Zugriff auf Methode via Dereferenzierung
    std::cout << petra->getAge() << std::endl; // Zugriff auf Methode via Pfeil

    std::cout << *pSepp << std::endl; // Dereferenzierung

    // NICHT VERGESSEN! ;-)
    delete petra; // oder: petra = nullptr;

    /* Der Destruktor vom unique_ptr ruft das delete für das "heidi"-Objekt auf.
    * Reihenfolge:
    * Destructor: (Petra,30)
    * Destructor: (Heidi,50)
    * Destructor: (Susi,44)
    * Destructor: (Sepp,33)
    */
    return 0;
```
