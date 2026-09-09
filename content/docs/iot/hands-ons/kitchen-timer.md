---
title : 'Kitchen Timer'
date : 2023-09-25T10:34:53+02:00
tags: ["draft"]
author: "Leon"
math: false
---

### Version 1.0

```mermaid
stateDiagram-v2
    [*] --> Init
    Init --> Init
    Init --> SetTime :Button pressed
    SetTime --> SetTime
    SetTime --> Running :Button pressed
    
    Running --> Running :Time not reached
    Running --> Finished :Time elapsed
    Running --> Init :Button pressed
    
    Finished --> Finished
    Finished --> Init :Button pressed
```

### Code

```C
// TODO
```


---

## Siehe auch

- → [State Machine](/docs/iot/hands-ons/state-machine) – Zustandsautomat als Grundmuster für Sketches
- → [Button Snippet](/docs/iot/snippets/button) – Taster einlesen
