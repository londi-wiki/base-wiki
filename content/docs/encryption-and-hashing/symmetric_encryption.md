---
weight: 999
title: "Symmetrische Verschlüsselung"
description: ""
icon: "article"
date: "2025-03-11T11:16:27+01:00"
lastmod: "2025-03-11T11:16:27+01:00"
draft: false
toc: true
katex: true
---


# SPN (Substitutionspermutationsnetzwerke)


Zutaten:
- Permutation auf {0, 1}^n (die S-Box)
- Selbstinverse Permutation B auf {0, 1, 2, m * n - 1} (die Bitpermutation)
- Rundenschlüsselfunktion K: {0, 1}^s x {0, 1, ..., r} -> {0, 1}^(m*n)

$ S: \{0, 1\}^n $

$ B: \{0, 1, 2, \dots, mn - 1\} $

$ K: \{0, 1\}^s \times \{0, 1, \dots, r\} \rightarrow \{0, 1\}^{mn} $


**Schlüsselgenerierung**

```
m = 3 (Anzahl S-Boxen pro Runde)
n = 4 (Blockgrösse der S-Box in Bits)
r = 3 (Anzahl Runden)
s = 24 (Schlüssellänge)

Es werden r+1 Schlüssel mit der länge n*m (12 Bits) erstellt.

k  = 0001 1010 1111 1100 0000 0111
k0 = 0001 1010 1111
k1 =      1010 1111 1100
k2 =           1111 1100 0000
k3 =                1100 0000 0111
```

**S-Box**

```
0000 -> 1110    //  0 -> E
0001 -> 0100    //  1 -> 4
0010 -> 1101    //  2 -> D
0011 -> 0001    //  3 -> 1
0100 -> 0010    //  4 -> 2
0101 -> 1111    //  5 -> F
0110 -> 1011    //  6 -> B
0111 -> 1000    //  7 -> 8
1000 -> 0011    //  8 -> 3
1001 -> 1010    //  9 -> A
1010 -> 0110    // 10 -> 6
1011 -> 1100    // 11 -> C
1100 -> 0101    // 12 -> 5
1101 -> 1001    // 13 -> 9
1110 -> 0000    // 14 -> 0
1111 -> 0111    // 15 -> 7
```

**Bit-Permutation**

```
β (Beta) Bit-Permutation

(Selbstinversiv)

 0 ->  4
 1 ->  5
 2 ->  6
 3 ->  7
 4 ->  0
 5 ->  1
 6 -> 10
 7 -> 11
 8 ->  2
 9 ->  3
10 ->  6
11 ->  7
```

## Verschlüsseln

```
-------- Initialer Weissschritt --------
                        1111 0101 0110
(xor)                   0001 1010 1111 k0
                        1110 1111 1001
--------  Erste Runde, regulär  --------
                        SBox SBox SBox
                          |    |    |
                          V    V    V
Bit-Permutation         0000 0111 0010
                        0100 0010 0011
(xor)                   1010 1111 1100 k1
-------- Zweite Runde, regulär  --------
                        SBox SBox SBox
                          |    |    |
                          V    V    V
Bit-Permutation         0000 1110 0111
                        1101 0011 0010
(xor)                   1111 1100 0000 k2
-------- Dritte Runde, verkürzt --------
                        SBox SBox SBox
                          |    |    |
                          V    V    V
                        1101 0111 1101
(xor)                   1100 0000 0111 k3
Chiffretext             0001 0111 1010

```

## Entschlüsseln

Beim Entschlüsseln wird die S-Box invertiert und die Schlüssel wie folgt vertauscht und verändert.

```
k  = 0001 1010 1111 1100 0000 0111
k0 = 0001 1010 1111
k1 =      1010 1111 1100
k2 =           1111 1100 0000
k3 =                1100 0000 0111

Bit-Permutation
 0 ->  4
 1 ->  5
 2 ->  6
 3 ->  7
 4 ->  0
 5 ->  1
 6 -> 10
 7 -> 11
 8 ->  2
 9 ->  3
10 ->  6
11 ->  7

- Erster und letzter Schlüssel werden direkt vertauscht
- die anderen Schlüssel werden mit in ihrer Reihenfolge vertauscht und Bit-Permutiert

k0 wird zu k3:                      1100 0000 0111 
k1 wird bit-permutiert und zu k2:   1100 1100 1100
k2 wird bit-permutiert und zu k1:   1111 1000 1011
k3 wird zu k0:                      0001 1010 1111
```

Mit diesen zwei Änderungen wird SPN wie beim Verschlüsseln angewendet.


# Modi

## ECB

Als Erstes wird der Klartext in Blöcke der Länge l unterteilt.
Jeder Block wird mit Schlüssel k mit xor verrechnet.

Grobes Vorgehen: `yi = E(xi, k)`

**Verschlüsseln**

```
Beispiel:
Vernam-System mit Länge l = 4
              x0   x1   x2
Klartext x = 0010 0110 1011
Schlüssel k = 0011


x0:     0010    x1:     0110    x2:     1011
k:      0011    k:      0011    k:      0011
(mod)   ----    (mod)   ----    (mod)   ----    
        0001            0101            1000
   
   
     y0   y1   y2
y = 0001 0101 1000
```

**Entschlüsseln**

```
Beispiel:
Vernam-System mit Länge l = 4
     y0   y1   y2
y = 0001 0101 1000
Schlüssel k = 0011


y0:     0001    y1:     0101    y2:     1000
k:      0011    k:      0011    k:      0011
(mod)   ----    (mod)   ----    (mod)   ----    
        0010            0110            1011
   
   
     x0   x1   x2
x = 0010 0110 1011
```


## R-CBC

Als Erstes wird der Klartext in Blöcke der Länge l unterteilt. 
Jeder Block wird mit dem jeweiligen vorherigen verschlüsselten Block mit xor verrechnet, 
wobei beim ersten Block für `y-1` ein Zufalls-Bitstring gewählt wird.

So ist jeder Block abhängig vom vorherigen Block.

Wichtig: y-1 muss beim Entschlüsseln bekannt sein.

Grobes Vorgehen: `yi = E(yi-1 (+) xi, k)`

**Verschlüsseln**

```
Beispiel:
Vernam-System mit Länge l = 3
Schlüssel k = 110
Zufallsstring y-1 = 001

             x0  x1  x2
Klartext x = 010 000 101


x0:     010     x1:     000     x2:     101
y-1:    001     y0:     101     y1:     011
(mod)   ---     (mod)   ---     (mod)   ---
        011             101             110
k:      110     k:      110     k:      110
(mod)   ---     (mod)   ---     (mod)   ---    
y0:     101     y1:     011     y2:     000     
   
   
    y-1 y0  y1  y2
y = 001 101 011 000
```

**Entschlüsseln**

```
Beispiel:
Vernam-System mit Länge l = 3
Schlüssel k = 110
Zufallsstring y-1 = 001

    y-1 y0  y1  y2
y = 001 101 011 000



y0:     101     y1:     011     y2:     000
k:      110     k:      110     k:      110
(mod)   ---     (mod)   ---     (mod)   ---
        011             101             110
y-1:    001     y0:     101     y1:     011
(mod)   ---     (mod)   ---     (mod)   ---     
x0:     010     x1:     000     x2:     101       
   
   
    x0  x1  x2 
x = 010 000 101
```


## R-CTR

Bei R-CTR wird wieder ein zufälliger Bitstring gewählt welcher pro Block um eins vergrössert wird.
Dieser Wert wird in die Verschlüsselungsfunktion E gegeben und das Resultat mit dem Block `xi` mit xor verrechnet.

Auch hier: y-1 muss beim Entschlüsseln bekannt sein.

Die Blöcke können somit unabhängig voneinander verschlüsselt werden (sogar parallel).

Grobes Vorgehen: `yi = E( (y-1 + i) mod 2^l ), k) (+) xi`

**Verschlüsseln**

```
Beispiel:
Vernam-System mit Länge l = 4
Schlüssel k = 0011
Zufallsstring y-1 = 1110

              x0   x1   x2
Klartext x = 0010 0110 1011


y-1:    1110    y-1:    1110    y-1:    1110
c:         0    c:         1    c:         2
(add)   ----    (add)   ----    (add)   ----
        1110            1111            0000
k:      0011    k:      0011    k:      0011
(mod)   ----    (mod)   ----    (mod)   ----    
        1101            1100            0011
x0:     0010    x1:     0110    x2:     1011
(mod)   ----    (mod)   ----    (mod)   ----
        1111            1010            1000      
   
   
    y-1   y0   y1   y2
y = 1110 1111 1010 1000
```

**Entschlüsseln**

Grobes Verfahren: `xi = yi (+) E((y-1 + i) mod 2^l, k)`

```
Beispiel:
Vernam-System mit Länge l = 4
Schlüssel k = 0011
Zufallsstring y-1 = 1110

    y-1   y0   y1   y2
y = 1110 1111 1010 1000

y-1:    1110    y-1:    1110    y-1:    1110
c:         0    c:         1    c:         2
(add)   ----    (add)   ----    (add)   ----
        1110            1111            0000
k:      0011    k:      0011    k:      0011
(mod)   ----    (mod)   ----    (mod)   ----    
        1101            1100            0011
y0:     1111    y1:     1010    y2:     1000
(mod)   ----    (mod)   ----    (mod)   ----
        0010            0110            1011      
   
   
     x0   x1   x2
x = 0010 0110 1011
```

## Vergleich

| Eigenschaft/Modi                               | ECB                               | R-CBC                                                                             | R-CTR                                                                                                                  |
|------------------------------------------------|-----------------------------------|-----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Grobes Vorgehen                                | Blöcke einzeln ver-/entschlüsseln | Blöcke abhängig vom vorherigen Block verschlüsseln, aber unabhängig entschlüsseln | Blöcke einzeln ver-/entschlüsseln aber abhängig von y-1                                                                |
| Verhalten von Übertragungsfehler bei einem Bit | max. 1 Bit in Block xi betroffen. | max. 1 Bit in Block xi betroffen.                                                 | Wenn Fehler in y-1, dann sind alle Blöcke betroffen, sonst max. 1 Bit in Block xi betroffen, wenn Fehler nicht in y-1. |


# SPN im CTR Modus

Wird SPN im CTR Modus betrieben, so wird beim Entschlüsseln die Verschlüsselungs-Funktion von SPN verwendet und nicht die Entschlüsselungsfunktion. Somit bleiben die S-Box und die Schlüssel unverändert.

$ x_i = E\left( \left( y_{i-1} + i \right) \bmod \, 2^l, \, k \right) \oplus y_i \quad (i = 0, \ldots, n - 1) $
