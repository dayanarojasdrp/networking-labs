# LAB 07 – SDN and BGP

## Objective

Understand modern networking concepts including SDN, VPC, and BGP.

---

## Network Models

### Traditional Network

* Control plane and data plane are integrated in network devices

### SDN (Software Defined Networking)

* Control plane is centralized
* Data plane is distributed across switches

### VPC (Virtual Private Cloud)

* Software-defined network in cloud environments (AWS, Azure)

---

## Control Plane vs Data Plane

* **Control Plane:** makes routing decisions (e.g., BGP)
* **Data Plane:** forwards packets based on those decisions

---

## OpenFlow

OpenFlow is a protocol that allows an SDN controller to communicate with network devices and define traffic behavior.

---

## BGP Overview

BGP (Border Gateway Protocol) is the protocol used to exchange routing information between autonomous systems.

---

## ASN (Autonomous System Number)

A unique identifier assigned to a network.

Example:

* AS65001
* AS65002

---

## ISP

An Internet Service Provider offers connectivity to the Internet.

---

## IXP

An Internet Exchange Point allows multiple networks to interconnect directly.

---

## BGP Lab Topology

* Router1 → AS65001 → 10.0.1.0/24
* Router2 → AS65002 → 10.0.2.0/24

---

## Configuration

### Router1

```bash
router bgp 65001
 neighbor 192.168.64.2 remote-as 65002
 network 10.0.1.0/24
```

### Router2

```bash
router bgp 65002
 neighbor 192.168.64.1 remote-as 65001
 network 10.0.2.0/24
```

---

## Verification

```bash
show ip bgp
```

---

## Key Takeaways

* SDN separates control and data planes
* VPC is an implementation of SDN in cloud
* BGP enables communication between different networks
* The Internet is built on interconnected autonomous systems
