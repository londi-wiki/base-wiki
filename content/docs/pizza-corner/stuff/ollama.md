---
weight: 999
title: "Ollama"
description: ""
icon: "article"
date: "2024-04-15T08:41:10+02:00"
lastmod: "2024-04-15T08:41:10+02:00"
draft: false
toc: true
---

# Ollama

Ollama ist ein CLI Tool um bekannte LLM Modelle auf eine Weise auszuprobieren.

## Anleitung

1. Ollama installieren
   1. Lokal: [Ollama Download Seite](https://ollama.com/download)
   2. Docker: https://hub.docker.com/r/ollama/ollama
      1. Hinweis: Für das Ausführen auf der GPU müssen zusätzliche Schritte gemacht werden, siehe Docker Seite.
      2. `docker exec -it ollama bash`
2. Starten, z.B. llama 2: `ollama run llama2`
3. Mit `/bye` beenden

[Verfügbare Modelle](https://ollama.com/library)
