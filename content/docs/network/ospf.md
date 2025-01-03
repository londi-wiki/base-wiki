---
weight: 999
title: "Ospf"
description: ""
icon: "article"
date: "2024-12-17T08:47:38+01:00"
lastmod: "2024-12-17T08:47:38+01:00"
draft: false
toc: true
---

# Open shortest path first (OSPF)

## Funktionsweise

OSP ist ein Link-State-Routing-Protokoll. Wichtigste Punkte:
1. Link-State-Datenbank: OSPF-Router sammeln Informationen über Netzwerk-Links (Kosten, Status) und 
erstellen eine Link-State-Datenbank (LSDB).
2. Dijkstra-Algorithmus: Basierend auf der LSDB berechnet OSPF die kürzesten Wege zu allen Zielen.
3. Hierarchisches Design: OSPF untersützt die Unterteilung in Areas, was dne Overhead reduziert.
4. Metrik: Die OSPD-Metrik basiert auf der **Kostenberechnung**. Standardmässig gilt:
5. OSPF-Nachrichten: Router tauschen Informationen über Hello, DBD, LSR, LSU und LSAck-Pakete aus.

**Kosten:** 
```
           Referenzbandbreite (100Mbps)
Kosten = -------------------------------
            Bandbreite der Verbindung
```

## OSPF Nachrichten

### Hello Packets

Aufbau und Aufrechterhaltung von Nachbarschaften

### Database description (DBD) packets

Überblick über die Datenbank synchronisieren

### Link-state request (LSR) packets

Anfordern fehlender Informationen

### Link-state update (LSU) packets

Austausch aktueller Informationen

### Link-state acknowledgment (LSAck) packets

Bestätigung des Empfangs von LSUs.


# Beispiel

![OSPF Example](https://wiki.strubli.com/images/ospf-example.png)

**Standorte:** R1, R2, R3 und deren zugehörige Router.
**ISP:** Verbindung zum Internet.
**Datenraten auf den WAN-Leitungen:**
- R2a – R2: 2 Mbps
- R2 – R3: 2 Mbps
- R3a – R3: 64 kbps

(Diese unterschiedlichen Bandbreiten beeinflussen die Kosten der OSPF-Links.)

## Router R1

```
Router(config)# router ospf 1                # Startet OSPF-Prozess 1
Router(config-router)# network 172.30.1.0 0.0.0.255 area 0
Router(config-router)# network 172.30.11.0 0.0.0.255 area 0
Router(config-router)# router-id 1.1.1.1

# Reload or use "clear ip ospf process" command, for this to take effect
R1#clear ip ospf process
```

## Router R2_a

```
Router(config)# router ospf 1                # Startet OSPF-Prozess 1
Router(config-router)# network 172.30.11.0 0.0.0.255 area 0
Router(config-router)# network 172.30.2.0 0.0.0.255 area 0
Router(config-router)# router-id 2.2.2.2

# Reload or use "clear ip ospf process" command, for this to take effect
R2_a#clear ip ospf process

# R2_a < 2000kbps > R2
R(config)# int s0/0/0
R(config-if)# bandwidth 2000

# Kosten= 100'000 / 2'000 = 50
```

## Router R2

```
Router(config)# router ospf 1                # Startet OSPF-Prozess 1
Router(config-router)# network 172.30.3.0 0.0.0.255 area 0
Router(config-router)# network 172.30.2.0 0.0.0.255 area 0
Router(config-router)# network 192.168.4.8 0.0.0.003 area 0
Router(config-router)# router-id 3.3.3.3

# Reload or use "clear ip ospf process" command, for this to take effect
R2#clear ip ospf process

# R2_a < 2000kbps > R2
R(config)# int s0/0/0
R(config-if)# bandwidth 2000

# Kosten= 100'000 / 2'000 = 50

# R2 < 64kbps > R3
R(config)# int s0/0/1
R(config-if)# bandwidth 64

# Kosten= 100'000 / 64 = 1'538
```

## Router R3

```
Router(config)# router ospf 1                # Startet OSPF-Prozess 1
Router(config-router)# network 192.168.4.8 0.0.0.003 area 0
Router(config-router)# network 192.168.4.12 0.0.0.003 area 0
Router(config-router)# network 192.168.5.0 0.0.0.003 area 0
Router(config-router)# router-id 4.4.4.4

# Reload or use "clear ip ospf process" command, for this to take effect
R3#clear ip ospf process
```

## Router R3_a

```
Router(config)# router ospf 1                # Startet OSPF-Prozess 1
Router(config-router)# network 172.30.11.0 0.0.0.255 area 0
Router(config-router)# network 192.168.4.12 0.0.0.003 area 0
Router(config-router)# router-id 5.5.5.5

# Reload or use "clear ip ospf process" command, for this to take effect
R3_a#clear ip ospf process
```

## Router R_ISP

```
Router(config)# router ospf 1                # Startet OSPF-Prozess 1
Router(config-router)# network 172.30.11.0 0.0.0.255 area 0
Router(config-router)# network 87.87.87.16 0.0.0.007 area 0
Router(config-router)# router-id 6.6.6.6

# Reload or use "clear ip ospf process" command, for this to take effect
R_ISP#clear ip ospf process

# static route: R_ISP <> ISP
R_ISP(config)# ip route 187.187.187.0 255.255.255.0 87.87.87.17
Router(config-router)# redistribute static subnets
```

## Router ISP

```
# static route: R_ISP <> ISP (wildcard back route)
R_ISP(config)# ip route 0.0.0.0 0.0.0.0 87.87.87.18
```

## Check

```
show ip ospf neighbor
show ip route ospf
show ip ospf
```

**ip route ospf**
```
R1#show ip route ospf
     87.0.0.0/29 is subnetted, 1 subnets
O       87.87.87.16 [110/65] via 172.30.11.4, 00:31:25, FastEthernet0/1
     172.30.0.0/24 is subnetted, 4 subnets
O       172.30.2.0 [110/51] via 172.30.11.2, 00:25:12, FastEthernet0/1
O       172.30.3.0 [110/52] via 172.30.11.2, 00:25:12, FastEthernet0/1
     187.187.0.0/24 is subnetted, 1 subnets
O E2    187.187.187.0 [110/20] via 172.30.11.4, 00:10:46, FastEthernet0/1
     192.168.4.0/30 is subnetted, 2 subnets
O       192.168.4.8 [110/1613] via 172.30.11.2, 00:23:59, FastEthernet0/1
O       192.168.4.12 [110/65] via 172.30.11.3, 00:36:59, FastEthernet0/1
O    192.168.5.0 [110/66] via 172.30.11.3, 00:36:59, FastEthernet0/1
```

**ip ospf neighbor**
```
R1#show ip ospf neighbor

Neighbor ID     Pri   State           Dead Time   Address         Interface
2.2.2.2           1   FULL/BDR        00:00:34    172.30.11.2     FastEthernet0/1
5.5.5.5           1   FULL/DROTHER    00:00:33    172.30.11.3     FastEthernet0/1
6.6.6.6           1   FULL/DROTHER    00:00:32    172.30.11.4     FastEthernet0/1
```


**ip ospf**
```
R1#show ip ospf
 Routing Process "ospf 1" with ID 1.1.1.1
 Supports only single TOS(TOS0) routes
 Supports opaque LSA
 SPF schedule delay 5 secs, Hold time between two SPFs 10 secs
 Minimum LSA interval 5 secs. Minimum LSA arrival 1 secs
 Number of external LSA 1. Checksum Sum 0x00aac8
 Number of opaque AS LSA 0. Checksum Sum 0x000000
 Number of DCbitless external and opaque AS LSA 0
 Number of DoNotAge external and opaque AS LSA 0
 Number of areas in this router is 1. 1 normal 0 stub 0 nssa
 External flood list length 0
    Area BACKBONE(0)
        Number of interfaces in this area is 2
        Area has no authentication
        SPF algorithm executed 17 times
        Area ranges are
        Number of LSA 8. Checksum Sum 0x03f15c
        Number of opaque link LSA 0. Checksum Sum 0x000000
        Number of DCbitless LSA 0
        Number of indication LSA 0
        Number of DoNotAge LSA 0
        Flood list length 0
```

**ip protocols**
```
R1#show ip protocols 

Routing Protocol is "ospf 1"
  Outgoing update filter list for all interfaces is not set 
  Incoming update filter list for all interfaces is not set 
  Router ID 1.1.1.1
  Number of areas in this router is 1. 1 normal 0 stub 0 nssa
  Maximum path: 4
  Routing for Networks:
    172.30.1.0 0.0.0.255 area 0
    172.30.11.0 0.0.0.255 area 0
  Routing Information Sources:  
    Gateway         Distance      Last Update 
    1.1.1.1              110      00:07:53
    2.2.2.2              110      00:02:27
    3.3.3.3              110      00:01:14
    4.4.4.4              110      00:00:59
    5.5.5.5              110      00:14:12
    6.6.6.6              110      00:18:03
  Distance: (default is 110)
```

**ip ospf interface f0/1**
```
R1#show ip ospf interface f0/1

FastEthernet0/1 is up, line protocol is up
  Internet address is 172.30.11.1/24, Area 0
  Process ID 1, Router ID 1.1.1.1, Network Type BROADCAST, Cost: 1
  Transmit Delay is 1 sec, State DR, Priority 1
  Designated Router (ID) 1.1.1.1, Interface address 172.30.11.1
  Backup Designated Router (ID) 2.2.2.2, Interface address 172.30.11.2
  Timer intervals configured, Hello 10, Dead 40, Wait 40, Retransmit 5
    Hello due in 00:00:03
  Index 2/2, flood queue length 0
  Next 0x0(0)/0x0(0)
  Last flood scan length is 1, maximum is 1
  Last flood scan time is 0 msec, maximum is 0 msec
  Neighbor Count is 3, Adjacent neighbor count is 3
    Adjacent with neighbor 2.2.2.2  (Backup Designated Router)
    Adjacent with neighbor 5.5.5.5
    Adjacent with neighbor 6.6.6.6
  Suppress hello for 0 neighbor(s)
```

## OSPF IPv6

```
Brugg(config)#ipv6 unicast-routing
Brugg(config)#ipv6 router ospf 1
Brugg(config-rtr)#router-id 1.1.1.1

Brugg(config)#int g0/1
Brugg(config-if)#ipv6 ospf 1 area 0

Brugg#show ipv6 protocols
IPv6 Routing Protocol is "connected"
IPv6 Routing Protocol is "application"
IPv6 Routing Protocol is "ND"
IPv6 Routing Protocol is "ospf 1"
  Router ID 1.1.1.1
  Number of areas: 1 normal, 0 stub, 0 nssa
  Interfaces (Area 0):
    Loopback0
    GigabitEthernet0/0
    Serial0/0/1
    GigabitEthernet0/1
  Redistribution:
    None
    

Brugg#show ipv6 ospf interface brief
Interface    PID   Area            Intf ID    Cost  State Nbrs F/C
Lo0          1     0               13         1     LOOP  0/0
Gi0/0        1     0               3          1     DR    1/1
Se0/0/1      1     0               7          64    P2P   1/1
Gi0/1        1     0               4          1     DR    0/0



Brugg#show ipv6 ospf neighbor

OSPFv3 Router with ID (1.1.1.1) (Process ID 1)

Neighbor ID     Pri   State           Dead Time   Interface ID    Interface
2.2.2.2           1   FULL/BDR        00:00:30    3               GigabitEthernet0/0
3.3.3.3           0   FULL/  -        00:00:35    6               Serial0/0/1



Brugg#show ipv6 route
IPv6 Routing Table - default - 7 entries
Codes: C - Connected, L - Local, S - Static, U - Per-user Static route
       B - BGP, HA - Home Agent, MR - Mobile Router, R - RIP
       H - NHRP, I1 - ISIS L1, I2 - ISIS L2, IA - ISIS interarea
       IS - ISIS summary, D - EIGRP, EX - EIGRP external, NM - NEMO
       ND - ND Default, NDp - ND Prefix, DCE - Destination, NDr - Redirect
       O - OSPF Intra, OI - OSPF Inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2, ls - LISP site
       ld - LISP dyn-EID, a - Application
O   2001:DB8:0:100::1/128 [110/64]
     via FE80::21B:D5FF:FE70:30D6, Serial0/0/1
O   2001:DB8:0:100::2/128 [110/1]
     via FE80::3A90:A5FF:FE38:7100, GigabitEthernet0/0
LC  2001:DB8:0:100::3/128 [0/0]
     via Loopback0, receive
O   2001:DB8:0:102::/64 [110/2]
     via FE80::3A90:A5FF:FE38:7100, GigabitEthernet0/0
C   2001:DB8:0:104::/64 [0/0]
     via GigabitEthernet0/1, directly connected
L   2001:DB8:0:104::1/128 [0/0]
     via GigabitEthernet0/1, receive
L   FF00::/8 [0/0]
     via Null0, receive

```
