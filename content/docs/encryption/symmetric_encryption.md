---
weight: 999
title: "Symmetric encryption"
description: ""
icon: "article"
date: "2025-03-11T11:16:27+01:00"
lastmod: "2025-03-11T11:16:27+01:00"
draft: false
toc: true
---


# SPN (Substitutionspermutationsnetzwerke)



# Modi

## ECB

```
Beispiel:



```

## R-CBC


Bei R-CBC wird ein Zufalls-Bitstring `y-1` gewählt welches. 

**Verschlüsseln**

```
Beispiel:
Vernam-System mit Länge l = 3
             x0  x1  x2
Klartext x = 010 000 101
Schlüssel k = 110
Zufallsstring y-1 = 001


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

    y-1 y0  y1  y2
y = 001 101 011 000

Schlüssel k = 110
Zufallsstring y-1 = 001


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


