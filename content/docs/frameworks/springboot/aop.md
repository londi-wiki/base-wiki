---
weight: 999
title: "Aop"
description: ""
icon: "article"
date: "2024-11-04T10:57:36+01:00"
lastmod: "2024-11-04T10:57:36+01:00"
draft: false
toc: true
---

# Was ist AOP?

Aspektorientierte Programmierung (AOP) ist ein Programmierparadigma
für die objektorientierte Programmierung, um generische
Funktionalitäten über mehrere Klassen hinweg zu verwenden
(Cross-Cutting Concern). Die Aspekte werden dabei von der
eigentlichen Geschäftslogik getrennt. Typische Anwendungsbeispiele
sind Transaktionsverwaltung, Auditfähigkeit oder Tracing.

## AOP Begriffe

- Aspect: A modularization of a
cross-cutting concern. The
combination of advice and
pointcut.
- Join Point: Point during the
execution of a program.
- Advice: Action taken at a
particular joinpoint.
- Pointcut: A set of joinpoints
specifying where advice should be
applied.
- Weaving: Assembling aspects into
advised objects.

TODO: Schema hinzufügen

## TODO AOP Code Generierung

TODO

## AspectJ Pointcut Expression

### Beispiel

```java
@Aspect
@Component
public class TraceAspect {
    private final Logger logger = LoggerFactory.getLogger(this.getClass());

    // Exercise 1
    @Before("execution(* *..customer..*.getAll*(..))")
    public void logGetAllBefore(JoinPoint p) {
        logger.debug("Called logGetAllBefore() before calling '{}'", p.getSignature());
    }
    // ...
}
```

```bash
* *..customer.web..*.getAll*(..)
↓ ↓  ↓       ↓   ↓  ↓     ↓   ↓
1 2  3       4   5  6     7   8

1. Erster *: Beliebiger Return-Typ
2. *..: Beliebiges Package und Sub-Packages vor "customer"
3. customer: Package-Name "customer"
4. web: Sub-Package "web"
5. ..: Beliebige weitere Sub-Packages nach "web"
6. *: Beliebiger Klassenname
7. getAll* - Alle Methoden die mit "getAll" beginnen
8. (..) - Beliebige Parameter
```

### Beispiel sammlung

```bash
// Nur bestimmter Return-Typ
"Customer *..customer.web..*.getCustomer(..)"
// trifft auf: Customer getCustomer()

// Bestimmte Parameter
"* *..customer.web..*.getCustomer(Long)"
// trifft auf: void getCustomer(Long id)

// Mehrere spezifische Parameter
"* *..customer.web..*.getCustomer(Long, String)"
// trifft auf: Customer getCustomer(Long id, String name)

// Bestimmtes Package ohne Wildcards
"* com.example.customer.web.*.getCustomer(..)"
// trifft nur auf Klassen direkt in com.example.customer.web

// Spezifische Klasse
"* *..customer.web.CustomerController.getCustomer(..)"
// trifft nur auf getCustomer in CustomerController
```

### Häufige Muster

```bash
// Alle Methoden in einem Package
"* com.example.service.*.*(..))"

// Alle getter Methoden
"* *.get*(..))"

// Alle Methoden mit bestimmter Annotation
"@annotation(org.springframework.transaction.annotation.Transactional)"

// Alle Methoden einer bestimmten Klasse
"* com.example.service.UserService.*(..))"

// Methoden die einen bestimmten Parameter-Typ haben
"* *..*(Long, ..)"  // Erster Parameter muss Long sein
```

## Parameter verändern

```java
@Around("@within(org.springframework.web.bind.annotation.RestController) && args(id)")
public Object traceServices(ProceedingJoinPoint pjp, Long id) throws Throwable {
    Object[] args = pjp.getArgs();
    logger.debug("Calling traceServices() before'{}' \nwith args: {}",
            pjp.getSignature(), args);
    args[0] = 2L;
    Object o = pjp.proceed(args);
    logger.debug("Calling traceServices() after'{}' \nwith args: {}",
            pjp.getSignature(), args);
    return o;
}
```