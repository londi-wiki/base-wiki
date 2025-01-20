---
weight: 999
title: "Use Cases"
description: ""
icon: "article"
date: "2025-01-20T02:05:00+02:00"
lastmod: "2025-01-20T02:05:00+02:00"
draft: false
toc: true
---

# Use Cases

## Automatisches starten stoppen von EC2 Instanzen

### AWS Lambda + CloudWatch Events

**Was ist es?**

Mit AWS Lambda können serverlose Funktionen erstellt werden, die Aktionen wie das Starten und Stoppen von EC2-Instanzen ausführen. 
Mithilfe von CloudWatch Events kannst du Zeitpläne oder bestimmte Trigger definieren, die die Lambda-Funktion auslösen.

**Wie funktioniert es?**

Es wird eine Lambda-Funktion erstellt, die die AWS SDK-Methoden startInstances und stopInstances aufruft. 
CloudWatch Events können als Zeitgeber fungieren, um diese Lambda-Funktion in bestimmten Intervallen auszuführen 
(z. B. täglich zu einer bestimmten Uhrzeit).

### Azure Automation

**Was ist es?**

Azure Automation ist ein Dienst, der es ermöglicht, Aufgaben wie das Starten und Stoppen von VMs automatisch zu steuern. 
Mit Runbooks (Skripten) können Aktionen wie das Starten oder Stoppen von Instanzen definieren werden.
