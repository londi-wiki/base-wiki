---
weight: 999
title: "Validation"
description: ""
icon: "article"
date: "2023-10-26T17:17:22+02:00"
lastmod: "2023-10-26T17:17:22+02:00"
draft: false
toc: true
---

## JSR-303 Annotations

```java

@NotNull
private String id;

@Size(min=5, max=20)
private String name;
```

```java
@RequestMapping(...)
public String create(@Valid Questionnaire questionnaire, BindingResult bindingResult, Model model) {
    if (bindingResult.hasErrors()){
        ...
    }    
}
```

