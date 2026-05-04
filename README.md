
# Networking Labs Portfolio

A comprehensive, hands-on networking lab portfolio demonstrating practical and theoretical expertise across modern networking, cloud infrastructure, DevOps, and Kubernetes environments.

This repository showcases real-world scenarios, from fundamental networking concepts to advanced topics such as TLS, SDN, and BGP.

---

## Overview

This project was developed as a complete learning and demonstration environment to simulate real-world networking scenarios under practical conditions.

It covers:

- IP addressing and subnetting (VLSM)
- Static routing
- NAT (SNAT, DNAT, PAT)
- Firewall configuration (iptables)
- IPv6 and dual-stack networking
- Cloud networking design (AWS, Azure, GCP)
- Kubernetes networking (CNI, Services, Ingress, Network Policies)
- Security concepts (TLS, SSL termination, PFS, STARTTLS)
- SDN (Software Defined Networking)
- BGP fundamentals (FRR, ASN, routing exchange)
- Network troubleshooting tools (nmap, tcpdump, curl, traceroute)

---

## Repository Structure

```

.
├── 01-ip-subnetting-routing-basics
├── 02-nat-firewall-and-diagnostics
├── 03-ipv6-and-dual-stack
├── 04-cloud-networking
├── 05-kubernetes-networking
├── 06-security-and-tls
├── 07-sdn-and-bgp
└── docs

```

Each lab includes:

- Documentation (README)
- Configurations
- Diagrams
- Practical examples

---

## Labs Breakdown

### Lab 01 – IP, Subnetting and Routing
- VLSM exercises
- Static routing with multiple routers (FRR)
- Network testing (ping, traceroute, ARP)

---

### Lab 02 – NAT, Firewall and Diagnostics
- SNAT, DNAT, PAT implementation
- iptables firewall rules
- Troubleshooting using:
  - nmap
  - tcpdump
  - curl
  - netstat

---

### Lab 03 – IPv6 and Dual Stack
- IPv4 + IPv6 configuration
- SLAAC and Router Advertisements
- Neighbor Discovery Protocol

---

### Lab 04 – Cloud Networking
- AWS, Azure, GCP architecture
- Public and private subnets
- Route tables and gateways
- Load balancing and VPC peering

---

### Lab 05 – Kubernetes Networking
- CNI fundamentals
- Services (ClusterIP, NodePort)
- Ingress routing (/api, /web)
- Network Policies (traffic control between pods)

---

### Lab 06 – Security and TLS
- Nginx reverse proxy
- HTTPS with self-signed certificates
- SSL termination
- TLS handshake validation using OpenSSL

---

### Lab 07 – SDN and BGP
- Traditional vs SDN vs VPC networking models
- Control Plane vs Data Plane
- OpenFlow fundamentals
- BGP simulation using FRR (multi-AS routing and exchange)

---

## Key Skills Demonstrated

- Network design and segmentation
- Routing and traffic flow analysis
- Infrastructure-level security (firewall + TLS)
- Service exposure (NodePort, Ingress)
- Reverse proxy architecture
- Distributed systems networking
- Troubleshooting and diagnostics
- Cloud and container networking concepts

---

## Tools & Technologies

- Docker
- FRRouting (FRR)
- Nginx
- iptables
- tcpdump / nmap / curl
- Kubernetes (Minikube / Kind)
- Linux networking tools

---

## Environment Constraints

This project was developed under constrained conditions:

- Limited or unstable internet access
- Pre-downloaded Docker images for offline use
- Partial simulation of certain cloud environments

Despite these limitations, all concepts were implemented, tested, or documented to reflect realistic behavior.

---

## Purpose

This repository was created to strengthen practical networking skills and simulate real-world infrastructure scenarios aligned with DevOps and Cloud Engineering roles.

---

## Conclusion

This project demonstrates the ability to:

- Design and implement network architectures
- Secure communication channels
- Troubleshoot complex networking issues
- Understand modern cloud-native networking environments

---

## Author

Dayana Rojas  
Computer Science Student  
```

---
