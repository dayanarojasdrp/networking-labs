# GCP Firewall Rules

## Overview
In Google Cloud Platform (GCP), firewall rules are applied at the **VPC level**, not directly to individual instances. They control inbound and outbound traffic based on IP ranges, protocols, ports, and instance tags.

---

## Common Firewall Rules

### 1. Web Server (Public Subnet)
- **Allow HTTP (tcp:80)** from `0.0.0.0/0`
- **Allow HTTPS (tcp:443)** from `0.0.0.0/0`
- **Allow SSH (tcp:22)** only from your trusted IP (e.g., `203.0.113.25`)

### 2. Database Server (Private Subnet)
- **Allow MySQL (tcp:3306)** only from instances with the tag `web-server`
- **Deny all inbound traffic** from `0.0.0.0/0`
- Outbound traffic allowed via **Cloud NAT**

### 3. Internal Communication
- **Allow ICMP (ping)** between all instances in the VPC for troubleshooting
- **Allow custom application ports** (e.g., `tcp:8080`) only between specific tags

---

## Example Rule Set

| Rule Name       | Direction | Protocol | Port   | Source/Destination | Action |
|-----------------|-----------|----------|--------|--------------------|--------|
| allow-http      | Ingress   | TCP      | 80     | 0.0.0.0/0          | Allow  |
| allow-https     | Ingress   | TCP      | 443    | 0.0.0.0/0          | Allow  |
| allow-ssh-admin | Ingress   | TCP      | 22     | 203.0.113.25       | Allow  |
| allow-mysql     | Ingress   | TCP      | 3306   | tag:web-server     | Allow  |
| deny-internet-db| Ingress   | All      | All    | 0.0.0.0/0          | Deny   |
| allow-outbound  | Egress    | All      | All    | 0.0.0.0/0          | Allow  |

---

## Key Differences with AWS and Azure
- **AWS Security Groups**: Applied at the instance level, stateful.  
- **Azure NSGs**: Applied at subnet or NIC level.  
- **GCP Firewall Rules**: Applied at the VPC level, using tags to target instances.  

---

## Best Practices
- Restrict SSH access to known IPs only.  
- Use tags to group instances and apply rules consistently.  
- Deny all inbound traffic to private subnets unless explicitly required.  
- Always allow outbound traffic from private subnets via Cloud NAT.  
