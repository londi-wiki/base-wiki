---
weight: 999
title: "Forms"
description: ""
icon: "article"
date: "2023-10-12T19:55:08+02:00"
lastmod: "2023-10-12T19:55:08+02:00"
draft: false
toc: true
---

```java
@RequestMapping(value = "", params = { "form" })
public String getForm(Model model) {
    model.addAttribute("questionnaire", new Questionnaire());
    return "questionnaires/create";
}
```

```java
@RequestMapping(value = "", method = RequestMethod.POST)
public String create(Questionnaire questionnaire) {
    this.questionnaireRepository.save(questionnaire);
    return "redirect:questionnaires";
}
```
