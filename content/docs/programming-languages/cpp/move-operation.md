---
weight: 999
title: "Move Operation"
description: ""
icon: "article"
date: "2024-10-19T14:36:55+02:00"
lastmod: "2024-10-19T14:36:55+02:00"
draft: false
toc: true
---

# Theorie

In c++ unterscheidet man bei den Speicheradressen grob zwischen L- und R-Values.

LValue (Left value) definiert eine identifizierbare Speicheradresse, RValue (Right value) hingegen einen temporärem Wert der nicht mit einem benannten Speicherort verknüpft ist.
RValues stehen meist auf der rechten Seite eines Zuweisungsoperators, z.B: Literale (5, 3.14, 'c'), Ausdrücke die temporäre Werte ergeben und Rückgabewerte von Funktionen.

Mit der Einführung von rvalue-Referenzen (erkennbar an &&) in C++11 wurde ein zusätzlicher Nutzen für rvalues geschaffen. Dies ermöglicht "Move-Semantics", also die Optimierung von Speicheroperationen, indem temporäre Objekte anstelle von Kopien übernommen werden. Ein Beispiel dafür ist:

```cpp
int&& r = 5; // 5 ist ein rvalue

// oder

std::vector<int> foo() {
    std::vector<int> vec = {1, 2, 3};
    return vec; // gibt ein rvalue zurück
}

std::vector<int> v = foo(); // der Rückgabewert wird verschoben statt kopiert (Move-Semantik)
```

Am besten versteht man lvalue als einen "benannten Speicherort" und rvalue als einen "temporären, anonymen Wert". rvalue-Referenzen erweitern dieses Konzept durch die Möglichkeit, temporäre Objekte effizienter zu handhaben.

## Beispiel

```cpp
#pragma once

#include <cassert>
#include <iostream>
#include <memory>
#include "Point.h"

class PointVector {
    size_t m_capacity; // die Grösse des Arrays auf dem Heap
    size_t m_size; // Anzahl Objekte im Array: m_size <= m_capacity
    std::unique_ptr<Point[]> m_data; // Zeiger auf den Heap

public:
    PointVector()
        : m_capacity(0)
          , m_size(0)
          , m_data(nullptr) {
        std::cout << "std-ctor" << std::endl;
    }

    // copy-ctor: deep copy
    PointVector(const PointVector& pv)
        : m_capacity(pv.m_capacity)
          , m_size(pv.m_size)
          , m_data(std::make_unique<Point[]>(m_capacity)) {
        // copy pv.m_data to m_data
        for (size_t i = 0; i < m_size; ++i) {
            m_data[i] = pv.m_data[i];
        }
        std::cout << "copy-ctor" << std::endl;
    }

    // assignment operator: deep copy
    PointVector& operator=(const PointVector& pv) {
        if (this != &pv) {
            m_capacity = pv.m_capacity;
            m_size = pv.m_size;
            m_data = std::make_unique<Point[]>(m_capacity);
            for (size_t i = 0; i < m_size; ++i) {
                m_data[i] = pv.m_data[i];
            }
        }
        std::cout << "assignment" << std::endl;
        return *this;
    }

    // move constructor
    /* 
     * exchange() setzt den wert von pv.m_capacity zu m_capacity und pv.m_capacity wird zu 0.
     * Bei m_data ruft exchange() automatisch move() auf.
     *
    */
    PointVector(PointVector&& pv) noexcept // noexcept heisst: wird keine exception werfen
        : m_capacity(std::exchange(pv.m_capacity, 0))
          , m_size(std::exchange(pv.m_size, 0))
          , m_data(std::exchange(pv.m_data, nullptr)) {
        std::cout << "move-ctor" << std::endl;
    }


    // move operator
    /* 
     * swap() tauscht die Werte und auch hier wird falls notwendig move() aufgerufen.
     * Das this-Objekt hat die Werte von pv erhalten. Dieses Objekt "lebt" dann noch im Scope weiter aber wird am Ende "geloescht".
    */
    PointVector& operator=(PointVector&& pv) noexcept {
        if (this != &pv) {
            std::swap(m_capacity, pv.m_capacity);
            std::swap(m_size, pv.m_size);
            std::swap(m_data, pv.m_data);
        }
        std::cout << "move" << std::endl;
        return *this;
    }

    size_t capacity() const { return m_capacity; }
    size_t size() const { return m_size; }
    bool empty() const { return m_size == 0; }

    const Point& front() const {
        assert(m_size > 0);
        return m_data[0];
    }

    const Point& back() const {
        assert(m_size > 0);
        return m_data[m_size - 1];
    }

    Point& front() {
        assert(m_size > 0);
        return m_data[0];
    }

    Point& back() {
        assert(m_size > 0);
        return m_data[m_size - 1];
    }

    void pushBack(const Point& p) {
        if (m_size == m_capacity) {
            // PointVector is full
            m_capacity = 2 * m_capacity + 1;
            auto data = std::make_unique<Point[]>(m_capacity);

            // copy m_data to data
            for (size_t i = 0; i < m_size; ++i) {
                data[i] = m_data[i];
            }

            m_data = std::move(data); // ownership movement
        }

        // add new point
        m_data[m_size++] = p;
    }

    friend std::ostream& operator<<(std::ostream& os, const PointVector& pv) {
        os << '[';
        if (!pv.empty()) os << pv.front();
        for (size_t i = 1; i < pv.m_size; ++i) {
            os << ',' << pv.m_data[i];
        }
        return os << ']';
    }
};
```

```cpp
#include <iostream>
#include <vector>

#include "PointVector.h"
using namespace std;

PointVector factory() {
    PointVector pv;
    pv.pushBack(Point{3, 4});
    pv.pushBack(Point{7, 8});
    pv.pushBack({12, 13});
    return pv;
}

// vector<PointVector> beispiel;

int main() {
    PointVector pv; // std-ctor
    cout << pv << endl;

    PointVector pv2 = factory(); // std-ctor
    cout << pv2 << endl;

    pv = factory(); // std-ctor + move
    cout << pv << endl;

    pv = move(pv2);
    pv.pushBack({55, 66});
    pv2.pushBack({77, 88});

    cout << "pv: " << pv << endl; // move
    cout << "p2: " << pv2 << endl; // move: pv2 ist nach wie vor in einem gueltigen Zustand, jedoch halt leer. Ausser bei swap(), dann erst am Schluss vom Scope.

    return 0;
}
```