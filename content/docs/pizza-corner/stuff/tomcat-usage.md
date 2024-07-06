---
title : 'Tomcat usage'
date : 2023-09-21T10:54:05+02:00
tags: ["draft"]
author: "Leon"
math: false
---

## Tomcat

```shell
catalina start
cataline stop
```

```shell
jar -tvf build/libs/ub1-solution.war 
```

```shell
sudo tail -99f /opt/tomcat/logs/catalina.out

# more detailed error logs:
sudo tail -99f /opt/tomcat/logs/localhost.2023-09-28.log
```

