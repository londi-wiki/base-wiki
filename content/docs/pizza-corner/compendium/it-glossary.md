---
weight: 999
title: "It Glossary"
description: ""
icon: "article"
date: "2024-02-19T08:42:55+01:00"
lastmod: "2025-05-24T23:27:00+02:00"
draft: false
toc: true
---

## Idempotent

English:
Idempotency, in the context of HTTP methods, refers to the characteristic of certain operations that can be applied multiple times without changing the result beyond the initial application. In simpler terms, an idempotent operation can be performed multiple times without changing the outcome after its first application. For example, deleting a specific item is idempotent because performing the delete operation multiple times on that item has the same effect as doing it once; the item remains deleted.

Deutsch:
Idempotenz, im Kontext von HTTP-Methoden, bezieht sich auf die Eigenschaft bestimmter Operationen, die mehrmals angewendet werden können, ohne das Ergebnis über die erste Anwendung hinaus zu ändern. In einfacheren Worten, eine idempotente Operation kann mehrmals durchgeführt werden, ohne das Ergebnis nach ihrer ersten Anwendung zu ändern. Zum Beispiel ist das Löschen eines bestimmten Elements idempotent, weil die mehrmalige Durchführung der Löschoperation auf dieses Element denselben Effekt hat wie das einmalige Durchführen; das Element bleibt gelöscht.

### Idempotente HTML Verben

- `GET`: Ruft eine Ressource ab, ohne sie zu verändern.
- `HEAD`: Ruft die Metadaten einer Ressource ab, ohne den Inhalt zu ändern.
- `PUT`: Aktualisiert eine Ressource, wobei die gleiche Anfrage immer das gleiche Ergebnis liefert.
- `DELETE`: Entfernt eine Ressource, wobei mehrfache Löschanfragen auf dasselbe Element keine weiteren Änderungen bewirken.
- `OPTIONS`: Gibt die unterstützten HTTP-Methoden für eine Ressource zurück, ohne sie zu verändern.
- `TRACE`: Führt eine diagnostische Anfrage aus, die keine Auswirkungen auf die Ressource hat.
- `CONNECT`: Etabliert eine Verbindung zu einem Server, ohne die Ressource zu verändern.
- `PATCH`: Aktualisiert eine Ressource teilweise, wobei die gleiche Anfrage immer das gleiche Ergebnis liefert.
- `POST`: In der Regel nicht idempotent, da es oft eine neue Ressource erstellt oder eine Aktion ausführt, die nicht wiederholt werden sollte.
