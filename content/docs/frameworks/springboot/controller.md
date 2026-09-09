---
weight: 999
title: "Controller"
description: ""
icon: "article"
date: "2023-10-12T19:53:59+02:00"
lastmod: "2023-10-12T19:53:59+02:00"
draft: false
toc: true
---




## Redirect a route

```java
@Controller
@RequestMapping("/")
public class IndexController {

    @RequestMapping(method = RequestMethod.GET)
    public String index() {
        return "redirect:questionnaires";
    }

}
```


---

## Siehe auch

- → [View](/docs/frameworks/springboot/view) – das Model an die View übergeben
- → [Forms](/docs/frameworks/springboot/forms) – Formulare an Objekte binden
- → [HTTP Servlets](/docs/distributed-systems/general/http-servlets-summary) – Servlet-Lebenszyklus, Thread-Sicherheit und web.xml
