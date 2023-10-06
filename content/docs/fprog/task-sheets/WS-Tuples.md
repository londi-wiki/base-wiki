---
title : 'WS Tuples'
date : 2023-09-24T17:40:54+02:00
tags: ["draft"]
author: "Leon"
math: false
---

### Task

```haskell
Arbeitsblatt: Tuples

> import Prelude hiding (fst, snd)

Tuples vs Classes

Eine Person könnte in Haskell wie folgt modelliert werden:

> type Person = (String, String, Int)

In Java würde man eine analoge Klasse so definieren:

class Person {
  String name;
  String phone;
  int age;
}

Eine Klasse welche drei Attribute hat. In Java müssen den Attributen jeweils Namen gegeben werden, in Haskell sind die Komponenten eines Tupels anonym.
Wir haben die Selektoren fst und snd kennengelernt. Sie funktionieren aber nur auf Paaren, also mit 2-Tuplen.
Ihre Definition ist sehr simpel:

> fst (a, b) = a
> snd (a, b) = b


Aufgabe 1: Zugriff auf ein bestimmtes Element

Wenn wir in unserem Person Tripel (ein Tupel mit 3 Komponenten) eine spezifische Komponente selektieren wollen, so können wir eine Funktion schreiben, die genau das tut:

> name :: Person -> String
> name (n, p, a) = n

Analog zu den Funktionen fst und snd definieren wir also ein Funktion name, welche die erste Komponente eines Person-Tupels ausliest.
Präziser: Es ist eine Funktion welche ein bestimmtes Muster (ein Tripel) erkennt und dann in der Lage ist,
einen Teil des erkannten Musters zurückzugeben. Mustererkennung heisst im Englischen „Pattern Matching“.
Wir werden davon in den nächsten Wochen noch mehrere und komplexere Beispiele sehen.

Nun können wir die Funktion auch nutzen:

> teacher :: Person
> teacher = ("Daniel Kröni", "056 202 78 17", 40)

a) Laden Sie dieses File in ghci
b) Testen Sie die Funktion name, indem Sie den Namen von teacher abfragen. Auf der Konsole sollte analog folgendes erscheinen:

name teacher
Daniel Kröni

c) Definieren Sie ein eigenes Tupel me, und fragen Sie auch dort den Namen ab. 
Hinweis: sie müssen den Code hier ergänzen und danach neu in GHCi laden.


> me :: Person
> me = ("Leon Lüthi", "079 123 45 67", 99)

d) Definieren Sie die Funktionen phone und age, welche Analog zu name die zweite bzw. dritte Komponente einer Person zurückgeben.

> phone :: Person -> String
> phone (n, p, a) = p

Man könnte auch die nicht verwendeten Parameter mit '_' ignorieren':
phone (_, p, _) = p

> age :: Person -> Int
> age (n, p, a) = a

e) Überprüfen Sie Ihre Funktionen phone und age indem Sie phone me und age me ausführen und sich vergewissern, dass die korrekten Werte zurückgegeben werden.

phone me
"079 123 45 67"

age me
99

Aufgabe 2 Tupel-Typen

a) Offensichtlich funktionieren die Funktionen fst und snd nicht mehr auf dem Person-Triple. Warum?

Die Funktion 'fst' erwartet ein Tuple aus zwei Werten. Person besteht aber aus drei Werten.
:t fst
fst :: (a, b) -> a

:info Person
type Person = (String, String, Int)


b) Warum funktionieren die Funktionen fst und snd nicht auf normalen Tripeln, die nicht vom Typ Person sind?
fst ("Hans", "0123456789", 23)

<interactive>:18:5:
    Couldn't match expected type `(a0, b0)'
                with actual type `([Char], [Char], t0)'
    In the first argument of `fst', namely `("Hans", "0123456789", 23)'
    In the expression: fst ("Hans", "0123456789", 23)
    In an equation for `it': it = fst ("Hans", "0123456789", 23)

c)	Schreiben Sie die Funktionen first, second und third welche die erste, zweite und dritte Komponente eines Tripels (a, b, c) zurückgeben.
Das Tripel soll nicht von einem bestimmten Typ sein.
Hinweis: Beginnen Sie mit der Typdeklaration der Funktion first und deklarieren Sie als Parameter den generischen Tupel Typ.


> first :: (a, b, c) -> a
> first (a, _, _) = a

> second :: (a, b, c) -> b
> second (_, b, _) = b

> third :: (a, b, c) -> c
> third (_, _, c) = c
```

### Output

```haskell
name me
"Leon L\252thi""
it :: String

> putStrLn (name me)
Leon Lüthi"
it :: ()
```