---
weight: 999
title: "View"
description: ""
icon: "article"
date: "2023-10-12T19:54:07+02:00"
lastmod: "2023-10-12T19:54:07+02:00"
draft: false
toc: true
---

## Use model

Inside the controller

```java
@RequestMapping(method = RequestMethod.GET)
public String findAll(Model model) {
    List<Questionnaire> questionnaires = questionnaireRepository.findAll();
    model.addAttribute("questionnaires", questionnaires);
    return "questionnaires/list";
}
```

---

## Siehe auch

- → [View Templates](/docs/frameworks/springboot/view-templates) – Fragmente und Layouts mit Thymeleaf
- → [Controller](/docs/frameworks/springboot/controller) – Routen und Redirects
