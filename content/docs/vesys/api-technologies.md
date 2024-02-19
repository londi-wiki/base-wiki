---
weight: 999
title: "Api Technologies"
description: ""
icon: "article"
date: "2024-02-19T08:28:51+01:00"
lastmod: "2024-02-19T08:28:51+01:00"
draft: false
toc: true
---

# API Technologies

## Overview

– Corba: RPC (Remote procedure call) framework
– RDA: Remote Data Access (querying DB over network)
– RMI: Remote Method Invocation (Java-only)
– XML-RPC: Simple RCP-Framework defined by Microsoft
– SOAP: Schema-based RCP-Framework
▪ Support of two communication styles: RPC and Document
– **REST**: APIs that are in harmony with the Web
– JSON-RPC: Take-over from XML
– ODATA: Same style as RDA. Client defines the shape of the result
– GraphQL: Client defines shape of the result
– gRPC: Focus on performance and Code generation

## Communication styles

### RPC

- Like local (in-process)
- typically, synchronous
- request and/or response could be a stream (asynchronous)

### Message based systems

- Information exchange through messages
    - Synchronous: message exchange over tcp or udp
    - Asynchronous: sender and receiver decoupled by message queue service

### Shared repository

- Tuple spaces: Processes can create, read and delete tuples
- Provides a small interface constisting of access primitives to the clients

## Remote APIs: Chalenges

### Heterogeneity

– Networks (big endian = network order / little endian)
    - 0x1122 = 4386 (17*256+34) or 8721 (34*256 + 17)
    - CR or CR LF (encoding)
– Computer hardware (Intel, AMD, ARM, ...)
– Operating System (unix, dos/windows, ...)
– Programming Language

#### Approaches

- Internet protocols to the rescue ;-)
    - Mask differences in underlying networks
- Middleware: Software layer that provides a programming abstraction as well as masking underlying (OS/HW) heterogeneity. 
    - In addition also cross language interoperability (Corba, SOAP, gRPC, GraphQL)

### Network latency

- A remote invocation in a distributed system takes considerably more time than an invocation in a non-distrubted system.
- This additional time delay must be taken into account

#### Approaches

- Transfer junks of data

### Error handling

- component can get overloaded, temporarily or for a long time
- component can get disconnected from the rest of the network
    - ACP-ACP-Problem
    - Challenge for the design of distributed protocols


#### Approaches

- Message corruption can be identified with a checksum
- Sequence numbers may enable you to detect a lost packet
- Idempotent operations simplify error handling


### Security

- Network security
    - Confidentiality: data can only be read by receiver (encryption)
    - Integrity: data was not changed
    - authenticity: data comes from person who claims to be the sender


#### Approaches

- Authentication (login) & Authorization (access rights)
    - Used to decide if person/program/device X has a cess to data/funnctionality/service Y
- Encrpytion of ddata in transit

### Scalability

– System remains effective when there is a significant increase in number of resources or users
– Cost of physical resources should scale at most linearly with the number of users

#### Approaches

– Clustering
– Preventing resources running out 
– log(n) data access

### Concurrency
– Concurrent execution arises naturally in distributed systems, particular on the server side
– Concurrent access to resources must be synchronized

#### Approaches
– Lock-Free programming (e.g. **NewIO**)
– Actor Systems

### Consistency

- Update consistency
    - Several processes access and update the system => Transactions
- Replication consistency
    - Replicating systems have to be updated after changes
- Cache consistency
    - Cache on client computer may keep data for subsequent reuse
- Clock consistency
    - Many algorithms depend on the us of (globally unique) time stamps

## Distributed Algorithms

### Concurrency / Non-determinism / No Global View
– No participating component (process, machine, ...) has complete 
information about the (overall) system
– Decisions must be taken based on incomplete information
– Nondeterministic: 
    - varying message runtime
    - diverging processor speeds
    - A node might fail
    - ...

### Example (GCD)

- Given a network of nodes where each node has a positive integer as its starting value
– The nodes only know their neighbors and have no information about the entire network. Each node can only send messages of any content to its neighbors.
– **Wanted**: An algorithm which computes the GCD of all start values

TODO: Mermaid of diagram

#### Approach

1. Send n to all neighbours
2. Receive x: 
    if x < n 
        - => wrong: n = n % x
        - => correct: (n-1) % x + 1
        - => after that: Send n to all neighbours

