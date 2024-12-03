---
weight: 999
title: "Cisco Ios"
description: ""
icon: "article"
date: "2024-11-02T13:47:10+01:00"
lastmod: "2024-11-02T13:47:10+01:00"
draft: false
toc: true
---

# Allgemein

CISCO IOS (Internetwork Operating System) ist das Betriebssystem von Routern und Switches des Unternehmens Cisco.

# Grundkonfiguration

## Hostname

```
Switch# configure terminal 
Switch(config)# hostname S_11 
S_11(config)# no hostname S_11 
```

## No DNS resolving

```
Switch# configure terminal 
Switch(config)# no ip domain-lookup
```

## PW für lokales Einloggen

```
S_11(config)# line console 0
S_11(config-line)# password cisco 
S_11(config-line)# login 

PW für entferntes Einloggen: 
S_11(config)# line vty 0 4
S_11(config-line)# password cisco
S_11(config-line)# login 
S_11(config-line)# transport input {telnet | ssh | all}
```

## PW für Übergang user mode – priviledged mode

```
Switch(config)# enable password class

oder mit Verschlüsselung des PW in der Konfiguration: 
Switch(config)# enable secret class

Verschlüsselung aller PW in der Konfiguration: 
Switch(config)# service password-encryption 
```

## Banner

```
S1(config)# banner motd " 
-------------------------
Authorized Access Only !!
-------------------------
"
```

## Konfiguration speichern

```
Switch# write memory
Switch# copy run start 
```

## Konfiguration löschen

```
Switch#write erase
```

# IP Adresse setzen

## IPv4

```
R1(config)# interface Serial 0/1/0
R1(config-if)# ip address 192.168.2.1 255.255.255.0
R1(config-if)# no shutdown
```

## IPv6

```
R1(config)# interface G0/0
R1(config-if)# ipv6 enable
R1(config-if)# ipv6 address 2001:0db8:0015:0001:0000:0000:0000:0001/64 eui-64
R1(config-if)# no shutdown
R1(config-if)# end
R1# show ipv6 interface brief
R1# show ipv6 route
R1# ping ipv6 2001:0db8:0015:0002:0000:0000:0000:0010
```

## Link-Local Address (LLA)

```
R1(config)# interface G0/0
R1(config-if)# ipv6 address FE80::1 link-local
```

## Show interface status

```
R1# show interfaces Serial 0/1/0
S1# show interface status
```

## Show mac address-table

```
Switch>enable
Switch#show mac address-table
```

## Show link-local address

```
Router# show ipv6 interface 

FastEthernet0/0 is up, line protocol is up
IPv6 is enabled, link-local address is FE80::210:11FF:FE72:7301
```

## Assign IP Address to a Switch

```
S1(config)# in vlan 1
S1(config-if)# ip address [IP-Adresse] [Subnetzmaske]
S1(config-if)# no shutdown
```

# Statische Route

## Route setzen

```
! Syntax: ip route [Ziel-Netzwerk] [Subnetzmaske] [Next-Hop-IP oder Ausgangs-Interface]
R1(config)# ip route 192.168.2.0 255.255.255.0 192.168.1.2

! Default Route (wird verwendet, wenn keine spezifischere Route passt)
R1(config)# ip route 0.0.0.0 0.0.0.0 192.168.1.1

! Überprüfen der konfigurierten Routen
R1(config)# do show ip route static

! Konfiguration speichern
R1(config)# do write memory
```

# Disable dynamic trunk

```java
switchport nonegotia?!
```
