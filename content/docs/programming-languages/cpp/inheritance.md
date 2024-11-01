---
weight: 999
title: "Inheritance"
description: ""
icon: "article"
date: "2024-11-01T15:43:52+01:00"
lastmod: "2024-11-01T15:43:52+01:00"
draft: false
toc: true
---


## Allgemein

**Einfache Vererbung:**

```cpp
// in h-Datei
class Person {
    string m_name; // Aggregation: Person hat einen Namen 
    int m_age; // Aggregation: Person hat ein Alter
    
public:
    Person(const char name[], int age) : m_name(name), m_age(age) {}
    string getName() const { return m_name; }
    void setAge(int age) { m_age = age; }
    void print() const; // keine inline-Implementierung
};

// in cpp-Datei
void Person::print() const {
    cout << "Name: " << m_name << endl; 
    cout << "Alter: " << m_age << endl; 
}

// -----

// in h-Datei: Vererbung: ein Student ist eine Person
class Student : public Person {
    // die Klasse Student wird von der Klasse Person abgeleitet 
    // und erbt alle Attribute und Methoden der Klasse Person 
    int m_number;
    
public:
    Student(const string& name, int age, int nr) 
    : Person(name, age), m_number(nr) {} 
    // neue Methoden der Klasse Student
    void setNumber(int nr) { m_number = nr; } 
    void printNumber() const;
};

// in cpp-Datei
void Student::printNumber() const {
    cout << "Studentennummer: " << m_number << endl;
}
```

## Konstruktoren in abgeleiteten Klassen

- Jeder abgeleitete Konstruktor initialisiert nur die neuen Attribute
- Vererbte Attribute werden vom Konstruktor der Basisklasse initialisiert
- falls kein expliziter Aufruf eines Konstruktors der Basisklasse erfolgt, wird der Standardkonstruktor der Basisklasse implizit aufgerufen (**falls vorhanden**)

```cpp
class Student : public Person {
...
public:
    Student(const string& name, int age, int nr) 
        : Person(name, age), m_number(nr) {} 
    ...
}
```

**Reihenfolge beachten:**
- Aufrufen von Konstruktoren der Basisklasse(n)
- Aufrufen von anderen Konstruktoren der eigenen Klasse (Constructor delegation) oder Initialisieren der eigenen Attribute

### using

Mit `using` können alle Konstruktoren der Basisklasse geerbt werden.

```cpp
class Student: public Person { 
int m_matNr = 0; // Initialwert ist hier wichtig

public:
    using Person::Person; // erbt alle Konstruktoren der Klasse Person 
    Student(const string& name, const string& vname, int m)
    : Person(name, vname), m_matNr(m) { 
        cout << "ctor von Student" << endl; 
    }
}
```

**Erklärung:**
- Das System verwendet den geerbten Konstruktor der Klasse Person und erzeugt einen Konstruktor für die Klasse Student mit der gleichen Deklaration. 
- Der erzeugte Konstruktor der Klasse Student ruft den Konstruktor der Klasse Person mit den gleichen Argumenten auf.


## Destruktor einer abgeleiteten Klasse

**Konzept**

- Der Destruktor einer abgeleiteten Klasse ruft nach Ausführung seines Methodenkörpers den Destruktor der Basisklasse implizit auf
- **Dynamische Attribute können im Destruktor zuerst gelöscht werden**, bevor Attribute der Basisklasse gelöscht werden

**Wann soll ein Destruktor ausprogrammiert werden?**

Wenn die Klasse Attribute enthält, welche eigenständig mit `new` erzeugt worden sind, 
so müssen diese im Destruktor wieder gelöscht werden

**Wird der Destruktor auch bei einem statisch erzeugten Objekt aufgerufen?**

Ja! Beim Verlassen des Blocks, in dem das Objekt erstellt worden ist,
wird zuerst der Destruktor aufgerufen, bevor das Objekt vom Stack
entfernt wird.

## Overload resolution

```cpp
class Vater {
public:
    void foo(char a) {
        std::cout << "Vater::foo(" << a << ")" << std::endl;
    }
};

class Sohn : public Vater {
public:
    using Vater::foo;
    void foo(int a) {
        std::cout << "Sohn::foo(" << a << ")" << std::endl;
    }
};

int main()
{
    Sohn s{};
    s.foo(5); // Sohn::foo(5)
    s.foo('A'); // Vater::foo(A)
}
```

## Typkonvertierungen von Zeigern

Typ einer Zeiger- oder Referenzvariable muss nicht gleich dem Typ
des Objektes sein, auf welches die Zeiger-/Referenzvariable verweist.

- bisher: `Student *pStud = new Student("Anna", 21, 50101);`
- neu: `Person *pPers = new Student("Anna", 21, 50101);`

### Implizite (automatische) Zeigerkonvertierung (Up-Cast)

```cpp
Person *pPers2 = pStud;
```

### Explizite Zeigerkonvertierung (Down-Cast)

```cpp
Student *pStud2 = dynamic_cast<Student*>(pPers);
```

**Up-Cast**
- Konvertierung in einen Zieltyp, der in der Vererbungshierarchie weiter oben liegt
- implizite Konvertierung
- immer gültig, wenn der Zieltyp ein Vorfahre ist

**Down-Cast**
- Konvertierung in einen Zieltyp, der in der Vererbungshierarchie weiter unten liegt
- nur explizite Konvertierung möglich
- nur gültig, wenn der Zeiger auf ein Objekt des Zieltyps oder einer abgeleiteten Klasse des Zieltyps zeigt

Beispiele:

```cpp
Person *pPers = new Person();
Student *pStud = new Student();

Person *pS = pStud; // impliziter Up-Cast
Student *pS2 = static_cast<Student*>(pS); // gültiger Down-Cast 
Student *pS3 = static_cast<Student*>(pPers); // ungültiger Down-Cast
```

**Anmerkung:**
Man kann nur zu einem spezifischeren Typ (Student) casten, 
wenn das Objekt tatsächlich von diesem Typ ist. 
Ein static_cast prüft dies zur Laufzeit nicht (anders als dynamic_cast), 
weshalb dieser Cast zwar kompiliert, **aber zu undefiniertem Verhalten führt**.


## Runtime Type Information (RTTI)

- Problem
  - static_cast oder C-Cast führen bei ungültigem Down-Cast zu Laufzeitfehlern
- RTTI
  - speichert genauen Typ zu jeder Instanz
  - kann bei Bedarf abgeschaltet werden
- dynamic_cast
  - bei einem gültigen Down-Cast
    - funktioniert wie ein static_cast
    - Student *pS4 = dynamic_cast<Student*>(pS); // pS4 == pS
  - bei einem ungültigen Down-Cast
    - gibt einen nullptr zurück (bei einer Zeigervariablen)
    - Student *pS5 = dynamic_cast<Student*>(pPers); // pS5 == nullptr
    - wirft bad_cast Exception (bei einer Referenzvariablen)

## Typkonvertierung mit Smart-Pointers

Funktioniert analog zu Zeigern.

```cpp
shared_ptr<Person> spP = make_shared<Person>();
shared_ptr<Person> spS = make_shared<Student>();

// gültige Down-Casts
auto sp1 = static_pointer_cast<Student>(spS); 
auto sp2 = dynamic_pointer_cast<Student>(spS);

// ungültiger Down-Cast
auto sp3 = dynamic_pointer_cast<Student>(spP); // sp3 == nullptr
```

## Typinformation bei RTTI

- Operator typeid
  - Syntax: `type_info& t = typeid(* Zeigervariable)`
  - gibt Referenz auf Typ-Informationsobjekt zurück
  - benötigt #include <typeinfo>

**Beispiel**:
```cpp
Person *pPers = new Person();
Person *pStud = new Student();
const type_info& tP = typeid(*pPers);
const type_info& tS = typeid(*pStud);
if (tP == tS) cout << "beide Typen sind gleich" << endl;
if (tP.before(tS)) cout << "tP ist eine Basisklasse von tS" << endl;
```

## Verdecken und Überschreiben

**Verdecken:**
- abgeleitete Klassen können Datenfelder
   enthalten, die den gleichen Namen haben wie
   Datenfelder in den Basisklassen, z.B. x
- sollte wenn möglich vermieden werden

**Überschreiben:**
- abgeleitete Klassen können Methoden
  enthalten, die die genau gleichen Signaturen
  haben wie Methoden in den Basisklassen
- wird sinnvoll eingesetzt




## Abstraktion



## Beispiel 1

```cpp
class Animal {
protected:
    std::string m_name;

public:
    explicit Animal(const std::string& name)
        : m_name(name) {
    }

    virtual ~Animal() {
        std::cout << "Animal(" << m_name << ") dtor" << std::endl;
    }

    virtual void say() = 0; // so wird die Funktion abstrakt
};

class Cat : public Animal {
public:
    // explicit Cat(const std::string& name)
    //     : Animal(name) {
    // }
    using Animal::Animal; // Konstruktor von Animal erben

    void say() override {
        std::cout << m_name << " says Meow" << std::endl;
    };

    ~Cat() override {
        std::cout << "Cat(" << m_name << ") dtor" << std::endl;
    }
};

class Dog : public Animal {
public:
    explicit Dog(const std::string& name)
        : Animal(name) {
    }

    void say() override {
        std::cout << m_name << " says Woof" << std::endl;
    };

    ~Dog() override {
        std::cout << "Dog(" << m_name << ") dtor" << std::endl;
    }
};

class Bird : public Animal {
public:
    explicit Bird(const std::string& name)
        : Animal(name) {
    }

    void say() override {
        std::cout << m_name << " says chirp" << std::endl;
    };

    ~Bird() override {
        std::cout << "Bird(" << m_name << ") dtor" << std::endl;
    }
};


int main() {
    std::array<std::unique_ptr<Animal>, 4> animals = {
        std::make_unique<Cat>("Milo"),
        std::make_unique<Dog>("Wilma"),
        std::make_unique<Dog>("Wiggles"),
        std::make_unique<Bird>("Charlie")
    };

    for (auto& animal : animals) {
        animal->say();
    }

    /*
    * Output:
    * Milo says Meow
    * Wilma says Woof
    * Wiggles says Woof
    * Charlie says chirp
    * Bird(Charlie) dtor
    * Animal(Charlie) dtor
    * Dog(Wiggles) dtor
    * Animal(Wiggles) dtor
    * Dog(Wilma) dtor
    * Animal(Wilma) dtor
    * Cat(Milo) dtor
    * Animal(Milo) dtor
     */
}
```