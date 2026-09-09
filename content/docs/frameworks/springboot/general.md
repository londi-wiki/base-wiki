---
weight: 999
title: "General"
description: ""
icon: "article"
date: "2023-10-12T19:53:48+02:00"
lastmod: "2023-10-12T19:53:48+02:00"
draft: false
toc: true
---

## Annotations

### @SpringBootApplication

### @RequestMapping(path="/", method = RequestMethod.GET)

- Front Controller
- @RequestMapping(path="/{id}", method = RequestMethod.GET)

### @Controller

- Page Controller

### @Autowired

...


### RequestParam vs. PathVariable

**RequestParam**

```java
@RequestMapping(value = "/questionnaire/", method = RequestMethod.GET)
public void findById(@RequestParam Long id) { ... }

// ...flashcard-mvc/questionnaire/?id=0
```

**PathVariable**

```java
@RequestMapping(value = "/questionnaire/{id}", method = RequestMethod.GET)
public void findById(@PathVariable("id") Long id) { ... }

// ...flashcard-mvc/questionnaire/0
```

---

## Siehe auch

- → [Spring Beans](/docs/frameworks/springboot/bean) – Beans und @Component
- → [@Autowired](/docs/frameworks/springboot/autowired) – Dependency Injection in Spring
- → [Controller](/docs/frameworks/springboot/controller) – Routen und Redirects
