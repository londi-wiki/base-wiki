---
weight: 999
title: "Repositpry"
description: ""
icon: "article"
date: "2024-01-16T19:53:59+02:00"
lastmod: "2024-01-16T19:53:59+02:00"
draft: false
toc: true
---

## Sort values

```java
    @RequestMapping(method = RequestMethod.GET)
    public String findAll(Model model) {
        Sort sort = Sort.by(Sort.Direction.ASC, "id");
        List<Questionnaire> questionnaires = questionnaireRepository.findAll(sort);
        model.addAttribute("questionnaires", questionnaires);
        return "questionnaires/list";
    }
```
