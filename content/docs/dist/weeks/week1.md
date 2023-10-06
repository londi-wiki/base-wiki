---
title : 'Week1'
date : 2023-09-19T21:18:01+02:00
tags: ["Zufallsexperiment", "Ergebnismenge", "Ereignis", "Elementarereignis"]
author: "Leon"
katex: true
---

# Laplace

[Definition Zufallsexperiment](/dist/general/zufallsexperiment)

[Wahrscheinlichkeit](/dist/general/wahrscheinlichkeit)

[Laplace Experiment](/dist/general/laplace-experiment)



# Grundlegende Regeln

## Produktregeln

Wenn es bei einem mehrstufigen Auswahlprozess für das 1. Objekt n1 Möglichkeiten, 
für das 2. Objekt n2 Möglichkeiten, ..., und für das k-te Objekt nk Möglichkeiten
gibt, dann gibt es für den gesamten Auswahlprozess n1 ° n2 ° ... ° nk Möglichkeiten.

### Veranschaulichung

Wir wählen zunächst eine Zahl zwischen 1 und 3 und anschliessend einen Vokal.

Wie viele Möglichkeiten gibt es?

**Mehrstufiger Auswahlprozess**

![mehrstufige-auswahl.png](/dist/mehrstufige-auswahl.png)

![mehrstufige-auswahl2.png](/dist/mehrstufige-auswahl2.png)

(Kartesisches Produkt)

### Beispiele

Wie viele Passwörter bestehend aus drei Kleinbuchstaben gibt es?

> {  }   {  }   {  }
> 
> 26    26    26
> 
> Produktregel: $26 \cdot 26 \cdot 26 = 26^{3}$

Wie viele Passwörter bestehend aus drei Kleinbuchstaben gibt es, 
wenn die ersten beiden Buchstaben verschieden sein müssen?

> {  }   {  }   {  }
>
> 26    25    26
>
> Produktregel: $26 \cdot 25 \cdot 26 = 26^{2} \cdot 25$

## Summenregel

Keine mehrstufige Auswahlprozesse sondern Objekte mit Eigenschaften bei dem kein Objekt dieselbe Eigenschaft hat.

### Beispiele

Eine Mietwagenfirma hat 5 Kleinwagen, 3 Mittelklassewagen und 2 Oberklassewagen.

> Da kein Auto sowohl Klein- und Mittelklasse- oder 
> Klein- und Oberklasse- oder 
> Mittel- und Oberklassewagen ist, 
> hat die Firma insgesamt 5 + 3 + 2 = 10 Wagen.

Wie viele Passwörter bestehend aus drei Zeichen gibt es,
die entweder nur aus Kleinbuchstaben oder nur aus Ziffern bestehen?

> {  }   {  }   {  }
>
> 26 26 26
> 
> Produktregel: $26 \cdot 26 \cdot 26 = 26^{3}$
> 
> {  }   {  }   {  }
>
> 10 10 10
> 
> Produktregel: $10 \cdot 10 \cdot 10 = 10^{3}$
> 
> **Total:**
> 
> Achtung! Die beiden "Bereiche" sind disjunkt, also kein Element gemeinsam und deshalb kann man die Summenregeln verwenden.
> 
> $26^{3} + 10^{3}$

Wie viele Passwörter bestehend aus drei Zeichen gibt es,
die aus genau zwei Kleinbuchstaben und einer Ziffer bestehen?

> { k }   { k }   { Z }
>
> 26 26 10
>
> Produktregel: $26 \cdot 26 \cdot 10 = 26^{2} \cdot 10$
> 
> { k }   { Z }   { k }
>
> 26 10 26
>
> Produktregel: $26 \cdot 26 \cdot 10 = 26^{2} \cdot 10$
> 
> { Z }   { k }   { k }
>
> 10 26 26
>
> Produktregel: $26 \cdot 26 \cdot 10 = 26^{2} \cdot 10$
> 
> Wichtig ist die Tatsache, dass die drei Mengen disjunkt sind. Nun kann wieder die Summenregeln verwendet werden:
> 
> $(10 \cdot 26^{2}) + (10 \cdot 26^{2}) + (10 \cdot 26^{2})$ Passwörter.
> 
> $3 \cdot (10 \cdot 26^{2})$ Passwörter.


## Lernkontrolle

Wie viele Passwörter bestehend aus drei Zeichen gibt es,
in denen genau ein 'a' vorkommt?

> { a }   { k\a }   { k\a }
>
> 1 25 25
>
> Produktregel: 1 \cdot 25 \cdot 25 = 25^{2}$
>
> Dies in drei verschiedenen Kombinationen. 
> Die Mengen sind disjunkt, weil das 'a' zur selben Zeit nur genau an einer Position sein darf und
> deshalb können diese Mengen mit der Summenregel addiert werden:
>
> $(25^{2}) + (25^{2}) + (25^{2})$
>
> $3 \cdot (25^{2})$ Passwörter

Wie viele Passwörter bestehend aus drei Zeichen gibt es,
in denen mindestens ein 'a' vorkommt?

> { 1 }   { k }   { k }
>
> 1 26 26
> 
> Produktregel: 1 \cdot 26 \cdot 26 = 26^{2}$
>
> Dies in drei verschiedenen Kombinationen. Die Mengen sind **nicht** disjunkt
> weil das 'a' zwar mindestens einmal vorkommen kann, dafür aber mehrmals.
> Zum Beispiel kommt das Passwort 'aaa' in allen drei Mengen vor.
> 
> Stattdessen können wir drei Eigenschaften definieren:
> 
> "mindestens 3 a" => "genau ein a" oder
> 
> "mindestens 3 a" => "genau zwei a" oder
> 
> "mindestens 3 a" => "genau drei a"
> 
> und diese Eigenschaften sind nun wieder disjunkt und können addiert werden
>
> "mindestens 3 a" => "genau ein a" ==> (siehe obere Aufgabe) ===> $3 \cdot (25^{2})$ Passwörter
>
> "mindestens 3 a" => "genau zwei a" ==> (siehe obere Aufgabe) ===> $3 \cdot 25$ Passwörter
>
> "mindestens 3 a" => "genau drei a" ==> 'aaa' ===> $1$ Passwort
> 
> Total: $3 \cdot (25^{2}) + 3 \cdot 25 + 1$ Passwörter
> 
> Alternativer Lösungsweg
> 
> "mindestens ein a" => Alle PW ohne die PW die kein 'a' enthalten.
> 
> Alle: 26 26 26 => $26^{3}$
> 
> PW ohne 'a': 25 25 25 => $25^{3}$
> 
> Somit: $26^{3} - 25^{3}$

