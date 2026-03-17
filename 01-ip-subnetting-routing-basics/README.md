# **LAB 01 – IP Subnetting and Static Routing**  
## *A Hands-On Networking Lab Using Docker and FRR*

---

## **Objective**

The goal of this lab is to demonstrate a solid understanding of fundamental networking concepts by building and configuring a multi-router topology, implementing static routing, and validating connectivity using standard diagnostic tools.

---

## **Activities Performed**

1. **VLSM Exercise Design** – Planned subnets for three LANs and two point-to-point links.
2. **Topology Construction** – Built a network with three routers (R1, R2, R3) using FRR in Docker containers.
3. **Static Routing Configuration** – Manually configured routing tables on all three routers.
4. **Connectivity Validation** – Used `ping`, `traceroute`, and `arp -a` to verify network behavior.
5. **Documentation** – Created a subnet table, network diagram, and explanatory notes.

---

## **Subnet Plan (VLSM)**

| Network | Subnet | Range | Usable IPs |
|--------|--------|-------|------------|
| LAN A | `172.20.0.0/26` | 172.20.0.0 – 172.20.0.63 | 62 |
| LAN B | `172.20.0.64/27` | 172.20.0.64 – 172.20.0.95 | 30 |
| LAN C | `172.20.0.96/28` | 172.20.0.96 – 172.20.0.111 | 14 |
| R1–R2 Link | `172.20.0.112/29` | 172.20.0.112 – 172.20.0.117 | 6 |
| R2–R3 Link | `172.20.0.128/29` | 172.20.0.128 – 172.20.0.133 | 6 |

---

## **Network Topology**

```
    LAN A (172.20.0.0/26)
        |
   172.20.0.2/26
        |
       R1
        | 172.20.0.114/29
        |
   172.20.0.115/29
        |              172.20.0.66/27
       R2 —————————————————-----------------LAN B  
        | 172.20.0.30/29                 172.20.0.64/27
        |
   172.20.0.31/29
        |
       R3
        |172.20.0.98/28
        |
     LAN C
 172.20.0.96/28

```

### Router Interface Assignments

**R1**
- `eth0`: 172.20.0.2/26 (LAN A)
- `eth1`: 172.20.0.114/29 (R1–R2 link)

**R2**
- `eth0`: 172.20.0.115/29 (R1–R2 link)
- `eth1`: 172.20.0.130/29 (R2–R3 link)
- `eth2`: 172.20.0.66/27 (LAN B)

**R3**
- `eth0`: 172.20.0.131/29 (R2–R3 link)
- `eth1`: 172.20.0.98/28 (LAN C)

---

## **Static Routing Configuration**

### R1
```
ip route 172.20.0.64/27 172.20.0.115
ip route 172.20.0.96/28 172.20.0.115
```

### R2
```
ip route 172.20.0.0/26 172.20.0.114
ip route 172.20.0.96/28 172.20.0.131
```

### R3
```
ip route 172.20.0.0/26 172.20.0.130
ip route 172.20.0.64/27 172.20.0.130
```

---

## **The Real Challenge: Environment Constraints**

This lab was built under unusual constraints.  
Living in Cuba, access to cloud platforms is extremely limited. Most providers block access from Cuban IPs or require credit cards and phone numbers that are simply not available.  

After trying several options without success, I decided to run the lab locally:

- **Hardware**: MacBook (host) + Linux VM with 6GB RAM and 2 cores (more than enough for this topology).
- **Connection**: SSH from my Mac terminal into the VM.
- **Tooling**: Docker + FRR inside the VM.

Despite the limited resources, the setup was stable and allowed full control over the network simulation.

---

## **The IP Assignment Confusion (And What I Learned)**

One of the biggest obstacles was a repeated `Address already in use` error when starting the containers.

At first, I couldn’t understand why Docker kept rejecting IPs that seemed perfectly available.  
The issue turned out to be **Docker’s default behavior**:

> When you create a custom bridge network, the **host itself takes the first usable IP** in that subnet.  
> For example, in `172.20.0.0/26`, the host reserves `172.20.0.1` for itself.

I had assigned that same IP to R1, causing the conflict.  
The fix was simple once understood:

 **Containers must use the *second* IP in each subnet**, starting from `.2` onward.

That one detail cost hours of debugging, but it clarified how Docker handles bridge networks and why the host always participates in the network.

---

## **Verification Tests**

### Ping Tests (All Successful)

```bash
# R1 → R2 (direct link)
docker exec r1 ping -c 2 172.20.0.115

# R2 → R3 (direct link)
docker exec r2 ping -c 2 172.20.0.131

# R1 → R3 (via R2)
docker exec r1 ping -c 2 172.20.0.98

# R3 → R1 (return path)
docker exec r3 ping -c 2 172.20.0.2
```

### ARP Table (R1 Example)

```bash
docker exec r1 arp -a
```

Output shows the MAC address of R2 and the host, confirming layer‑2 connectivity.

---

## **Conclusions**

- The lab successfully demonstrates static routing and IP subnetting.
- Docker + FRR is a lightweight and effective way to simulate complex networks.
- Understanding how Docker assigns IPs to the host is critical to avoiding conflicts.
- Even with geographic and resource limitations, a fully functional network lab is possible using local virtualization.

---

## **Next Steps**

Proceed to **LAB 02**, where we will extend this topology with NAT, firewall rules, and diagnostic tools like `tcpdump` and `nmap`.
## IP address assignment per router

### Router R1
| Interfaz | Red | IP |
|----------|------|------|
| R1-LAN-A | LAN A | 172.20.0.2/26 |
| R1-R2    | Enlace R1–R2 | 172.20.0.114/29|

### Router R2
| Interfaz | Red | IP |
|----------|------|------|
| R2-LAN-B | LAN B | 172.20.0.66/27 |
| R2-R1 | Enlace R1–R2 | 172.20.0.115/29 |
| R2-R3 | Enlace R2–R3 | 172.20.0.130/29 |

### Router R3
| Interfaz | Red | IP |
|----------|------|------|
| R3-R2    | Enlace R2–R3 | 172.20.0.131/29 |
| R3-LAN-C | LAN C | 172.20.0.98/28 |

