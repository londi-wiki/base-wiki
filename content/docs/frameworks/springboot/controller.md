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
