---
weight: 999
title: "Bean"
description: ""
icon: "article"
date: "2024-09-17T08:25:04+02:00"
lastmod: "2024-09-17T08:25:04+02:00"
draft: false
toc: true
---

# Spring Beans

## Component

Mit `@Component` markiert man eine Klasse als Spring Bean
```java
@Target(TYPE) // Type: Klasse, Interface, Enum
@Retention(RUNTIME) // Runtime, Class, Source (nur für compiler), Runtime
@Documented // Javadoc
@Indexed // Springboot Meta Annotation: Performance Verbesserung
public @interface Component {
    String value() default ""; // Wird meist leer gelassen
}
```

Ähnliche Meta Annotationen wie Component sind folgende:

- @Service: Für Business Logik
- @Controller: Web Controller
- @Repository: Datenbanken
- @Configuration: Konfigurationen

Obwohl diese eher "kosmetischer Natur" sind, gibt es dennoch Unterschiede beim Verhalten, 
da der Assembler einen eingeschränkten Scanning Scope haben könnte.



