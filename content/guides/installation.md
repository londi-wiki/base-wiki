---
title : 'Installation'
date : 2023-09-21T10:53:57+02:00
tags: ["draft"]
author: "Leon"
math: false
---

## Java min. 11.x

```shell
sudo apt install openjdk-19-jdk-headless
```

## Gradle min 4.x

```shell
wget https://services.gradle.org/distributions/gradle-8.3-bin.zip -P /tmp
sudo unzip -d /opt/gradle /tmp/gradle-8.3-bin.zip
sudo ln -s /opt/gradle/gradle-8.3 /opt/gradle/latest

> sudo nano /etc/profile.d/gradle.sh
export GRADLE_HOME=/opt/gradle/latest
export PATH=${GRADLE_HOME}/bin:${PATH}

sudo chmod +x /etc/profile.d/gradle.sh
source /etc/profile.d/gradle.sh

gradle -v
```

## Tomcat min 10.x

[DigitalOcean Anleitung](https://www.digitalocean.com/community/tutorials/how-to-install-apache-tomcat-10-on-ubuntu-20-04)

```shell
sudo useradd -m -d /opt/tomcat -U -s /bin/false tomcat
wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.13/bin/apache-tomcat-10.1.13.tar.gz -P /tmp

sudo tar xzvf /tmp/apache-tomcat-10*tar.gz -C /opt/tomcat --strip-components=1

sudo chown -R tomcat:tomcat /opt/tomcat/
sudo chmod -R u+x /opt/tomcat/bin

> sudo nano /opt/tomcat/conf/tomcat-users.xml
...
    <role rolename="manager-gui" />
    <user username="manager" password="manager123" roles="manager-gui" />
    
    <role rolename="admin-gui" />
    <user username="admin" password="admin123" roles="manager-gui,admin-gui" />

</tomcat-users>

> sudo nano /opt/tomcat/webapps/manager/META-INF/context.xml
comment out valve value
> sudo nano /opt/tomcat/webapps/host-manager/META-INF/context.xml
comment out valve value

# Show location of java
sudo update-java-alternatives -l

> sudo nano /etc/systemd/system/tomcat.service

[Unit]
Description=Tomcat
After=network.target

[Service]
Type=forking

User=tomcat
Group=tomcat

Environment="JAVA_HOME=/usr/lib/jvm/java-1.19.0-openjdk-amd64"
Environment="JAVA_OPTS=-Djava.security.egd=file:///dev/urandom"
Environment="CATALINA_BASE=/opt/tomcat"
Environment="CATALINA_HOME=/opt/tomcat"
Environment="CATALINA_PID=/opt/tomcat/temp/tomcat.pid"
Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"

ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh

RestartSec=10
Restart=always

[Install]
WantedBy=multi-user.target



sudo systemctl daemon-reload
sudo systemctl start tomcat
sudo systemctl status tomcat
sudo systemctl enable tomcat
```