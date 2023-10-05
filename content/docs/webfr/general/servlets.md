---
title : 'Servlets'
date : 2023-09-28T17:39:25+02:00
tags: ["week2"]
author: "Leon"
math: false
---

## Filter

Filter modifizieren das Verhalten jedoch ohne dass das Servlet verändert wird.

- Interceptor
- Chain of Responsibility (Handler)

### Filter Mapping

- Werden im web.xml definiert
  - Reihenfolge relevant
  - Servlets auf welche ein Filter angewendet wird kann definiert werden
- chain.doFilter(request, response, filterChain)

## Listener

- Servlet Context
- Servlet Context Attribute
- Http Session Attribute
- Http Session Binding

> Werden im web.xml definiert.


