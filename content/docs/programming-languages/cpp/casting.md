---
weight: 999
title: "Casting"
description: ""
icon: "article"
date: "2024-11-01T15:23:24+01:00"
lastmod: "2024-11-01T15:23:24+01:00"
draft: false
toc: true
---

## Beispiel 1

```cpp
struct Parent {
    virtual void f() { std::cout << "Parent::f" << std::endl; }
    void g() { std::cout << "Parent::g" << std::endl; }
};

struct Self : public Parent {
    void f() override { std::cout << "Self::f" << std::endl; }
    void g() { std::cout << "Self::g" << std::endl; }
};

struct Child : public Self {
    void f() override { std::cout << "Child::f" << std::endl; }
    void g() { std::cout << "Child::g" << std::endl; }
};

int main()  {
    Self ss; Parent* p = &ss;
    if(p != nullptr) { std::cout << "A" << std::endl; }

    Self* s = static_cast<Self*>(p);
    if(s != nullptr) { std::cout << "B" << std::endl; }

    Child* c = static_cast<Child*>(p);
    if(c != nullptr) { std::cout << "C" << std::endl; }

    s = dynamic_cast<Self*>(p);
    if(s != nullptr) { std::cout << "D" << std::endl; }

    c = dynamic_cast<Child*>(p);
    if(c != nullptr) { std::cout << "E" << std::endl; }
}
```

### Erklärung

Lass uns das schrittweise durchgehen:

1) Der Grund, warum "E" nicht ausgegeben wird, liegt an der Verwendung von `dynamic_cast` im letzten Fall.

2) Schauen wir uns die Situation an:
    - Wir haben ein Objekt vom Typ `Self` (`ss`)
    - Dieses wird über einen `Parent*` Zeiger referenziert
    - Dann versuchen wir verschiedene Casts

3) Die wichtigen Unterschiede:

    - `static_cast` führt die Umwandlung ohne Laufzeitprüfung durch. Es vertraut einfach darauf, dass der Programmierer weiss, was er tut.

    - `dynamic_cast` hingegen prüft zur Laufzeit, ob die Umwandlung gültig ist. Bei Zeigern gibt es `nullptr` zurück, wenn die Umwandlung nicht möglich ist.

4) In diesem Fall:
    - Das Objekt ist tatsächlich vom Typ `Self`
    - Der Versuch, es zu `Child` zu casten, ist eigentlich nicht korrekt, da das Objekt kein `Child`-Objekt ist
    - `static_cast` macht es trotzdem (deshalb wird "C" ausgegeben)
    - `dynamic_cast` erkennt, dass dies keine gültige Umwandlung ist und gibt `nullptr` zurück

Daher ist `c` im letzten Fall `nullptr` und die Bedingung `if(c != nullptr)` ist nicht erfüllt - folglich wird "E" nicht ausgegeben.

Dies ist ein gutes Beispiel dafür, warum `dynamic_cast` sicherer ist als `static_cast`, wenn man mit Vererbungshierarchien arbeitet. `static_cast` kann zu undefiniertem Verhalten führen, wenn man fälschlicherweise zu einem falschen Typ castet, während `dynamic_cast` solche Fehler zur Laufzeit erkennt.
