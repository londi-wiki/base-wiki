---
weight: 999
title: "Mysql Snippets"
description: ""
icon: "article"
date: "2024-01-02T16:53:31+01:00"
lastmod: "2024-01-02T16:53:31+01:00"
draft: false
toc: true
---

## Add user

```mysql
CREATE USER 'sammy'@'localhost' IDENTIFIED WITH authentication_plugin BY 'password';
CREATE USER 'sammy'@'localhost' IDENTIFIED BY 'password';
CREATE USER 'sammy'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
ALTER USER 'sammy'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

## Granting access

```mysql
GRANT PRIVILEGE ON database.table TO 'bibliotest'@'mysql-1';
GRANT CREATE, ALTER, DROP, INSERT, UPDATE, INDEX, DELETE, SELECT, REFERENCES, RELOAD ON *.* TO 'sammy'@'localhost' WITH GRANT OPTION;
GRANT CREATE, ALTER, DROP, INSERT, UPDATE, INDEX, DELETE, SELECT, REFERENCES ON DATBASEXY.* TO 'sammy'@'localhost';
FLUSH PRIVILEGES;
```

## mysql command history

```bash
cat ~/.mysql_history
```