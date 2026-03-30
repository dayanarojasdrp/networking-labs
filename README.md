#  Networking  Labs

This repository contains a comprehensive, hands-on networking lab series designed to demonstrate practical and theoretical knowledge across modern networking, cloud, DevOps, and Kubernetes environments.

It covers everything from fundamental networking concepts to advanced topics such as TLS, SDN, and BGP.

---

##  Overview

This project was built as a complete learning and demonstration environment to simulate real-world networking scenarios.

It includes:

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

##  Repository Structure
```
.
├── 01-ip-subnetting-routing-basics
│   ├── README.md
│   ├── configs
│   │   ├── r1
│   │   │   ├── daemons
│   │   │   ├── frr.conf
│   │   │   ├── frr.conf.dpkg-dist
│   │   │   ├── support_bundle_commands.conf
│   │   │   └── vtysh.conf
│   │   ├── r2
│   │   │   ├── daemons
│   │   │   ├── frr.conf
│   │   │   ├── frr.conf.dpkg-dist
│   │   │   ├── frr.conf.sav
│   │   │   ├── support_bundle_commands.conf
│   │   │   └── vtysh.conf
│   │   └── r3
│   │       ├── daemons
│   │       ├── frr.conf
│   │       ├── frr.conf.dpkg-dist
│   │       ├── support_bundle_commands.conf
│   │       └── vtysh.conf
│   ├── diagrams
│   │   └── Networking.jpeg
│   └── docker-compose.yml
├── 02-nat-firewall-and-diagnostics
│   ├── README.md
│   ├── captures
│   │   ├── curl.jpeg
│   │   ├── curl1.jpeg
│   │   ├── nmap.jpeg
│   │   ├── ss.jpeg
│   │   └── tcpdump.jpeg
│   └── iptables
│       └── rules.md
├── 03-ipv6-and-dual-stack
│   ├── README.md
│   ├── catches
│   │   ├── Catche1.jpeg
│   │   └── Catche2.jpeg
│   └── configs
│       ├── docker-ipv6-limitations.txt
│       ├── r2-frr.conf
│       └── r2-linux-ipv6.txt
├── 04-cloud-networking
│   ├── README.md
│   ├── aws
│   │   ├── AWS.jpeg
│   │   ├── Load-Balancer.jpeg
│   │   ├── Load-Balancer.md
│   │   ├── VPC-Peering.jpeg
│   │   └── vpc-peering-route-tables.md
│   ├── azure
│   │   ├── Azure.jpeg
│   │   └── Azure.md
│   └── gcp
│       ├── GCP.jpeg
│       └── GCP.md
├── 05-kubernetes-networking
│   ├── README.md
│   ├── diagrams
│   └── manifests
│       ├── deployments
│       │   ├── backend.yaml
│       │   ├── db.yaml
│       │   └── frontend.yaml
│       ├── ingress
│       │   └── ingress.yaml
│       ├── policies
│       │   ├── allow-backend-db.yaml
│       │   ├── allow-frontend-backend.yaml
│       │   └── default-deny.yaml
│       └── services
│           ├── backend.yaml
│           ├── db.yaml
│           └── frontend.yaml
├── 06-security-and-tls
│   ├── README.md
│   ├── certs
│   │   └── cert.pem
│   └── nginx
│       └── nginx.conf
├── 07-sdn-and-bgp
│   ├── README.md
│   ├── diagrams
│   │   ├── BGP-Topology.jpeg
│   │   ├── Control-Plane-vs-Data-Plane.jpeg
│   │   └── traditional-vs-sdn-vpc.jpeg
│   └── frr
│       ├── explanation.md
│       ├── router1.conf
│       └── router2.conf
└── docs
    └── global-diagram.drawio
```
Each lab includes:

-  Documentation (README)
-  Configurations
-  Diagrams
-  Practical examples

---

##  Labs Description

### Lab 01 – IP, Subnetting and Routing
- VLSM exercises
- Static routing with multiple routers (FRR)
- Network testing (ping, traceroute, ARP)

---

###  Lab 02 – NAT, Firewall and Diagnostics
- SNAT, DNAT, PAT implementation
- iptables firewall rules
- Troubleshooting using:
  - nmap
  - tcpdump
  - curl
  - netstat

---

###  Lab 03 – IPv6 and Dual Stack
- IPv4 + IPv6 configuration
- SLAAC and Router Advertisements
- Neighbor Discovery Protocol

---

###  Lab 04 – Cloud Networking
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

###  Lab 06 – Security and TLS
- Nginx reverse proxy
- HTTPS with self-signed certificates
- SSL termination
- TLS handshake validation using OpenSSL

---

### Lab 07 – SDN and BGP
- Traditional vs SDN vs VPC networking models
- Control Plane vs Data Plane
- OpenFlow fundamentals
- BGP simulation using FRR (two routers, two ASNs, route exchange)

---

##  Environment Constraints

Due to geographic and infrastructure limitations, this project was developed under constrained conditions:

- Limited or unstable internet access
- Docker images had to be pre-downloaded and reused locally
- Some labs were partially simulated instead of fully deployed

Despite these limitations, all concepts were implemented, tested, or accurately documented to reflect real-world behavior.

---

##  Key Concepts Demonstrated

- Network design and segmentation
- Traffic flow and routing logic
- Security layers (firewall + TLS)
- Service exposure (NodePort, Ingress)
- Reverse proxy architecture
- Control vs data plane separation
- Internet routing fundamentals (BGP)

---

##  Tools Used

- Docker
- FRRouting (FRR)
- Nginx
- iptables
- tcpdump / nmap / curl
- Kubernetes (minikube / kind)
- Linux networking tools

---

##  Conclusion

This repository demonstrates practical networking knowledge aligned with real-world DevOps, Cloud, and Infrastructure roles.

It reflects the ability to:

- Design networks
- Secure traffic
- Debug connectivity issues
- Understand modern distributed systems

---

##  Author

Developed as part of a hands-on networking learning path focused on real-world infrastructure and cloud environments.
