---
weight: 999
title: "Multiple Ssh Keys"
description: ""
icon: "article"
date: "2023-11-20T19:42:02+01:00"
lastmod: "2023-11-20T19:42:02+01:00"
draft: false
toc: true
---

```bash
 #user1 account
 Host bitbucket.org-user1
     HostName bitbucket.org
     User git
     IdentityFile ~/.ssh/user1
     IdentitiesOnly yes

 #user2 account
 Host bitbucket.org-user2
     HostName bitbucket.org
     User git
     IdentityFile ~/.ssh/user2
     IdentitiesOnly yes
     
 Host github.com
    Hostname ssh.github.com
    Port 443
    ...
```

---

## Siehe auch

- → [SSH Kommandos](/docs/pizza-corner/stuff/ssh-commands) – Hostkeys, SOCKS-Proxy und ssh-copy-id
- → [Nützliche Git-Befehle](/docs/pizza-corner/git/useful-git-commands) – Dateien aus der History entfernen und mehr
