

# LAB 02 – Advanced NAT, Firewall, and Network Diagnostics

## Objective
Implement a border router capable of performing Source NAT (SNAT), Destination NAT (DNAT), Port Address Translation (PAT), and firewall filtering using iptables.  
Validate and troubleshoot traffic using professional diagnostic tools.

This lab simulates a real-world scenario where an internal network is protected and selectively published to the Internet.

---

## Topology
- **LAN A**: Internal network with client hosts  
- **R2**: Border router performing NAT and firewall filtering  
- **LAN B**: Internal network hosting a web server (nginx)  
- **Internet**: External network simulated by the host machine  

---

## 1. SNAT / PAT – Internet Access for Internal Clients

### Rule applied on R2
```
iptables -t nat -A POSTROUTING -s 172.20.0.0/26 -o eth0 -j MASQUERADE
```

### Explanation
- **SNAT** replaces the source IP of internal hosts with the router’s public IP.
- **PAT** allows multiple internal clients to share a single public IP using port translation.
- **MASQUERADE** dynamically uses the router’s external IP.

### Validation
From a host in LAN A:
```
curl http://example.com
```

---

## 2. DNAT – Publishing an Internal Server

### Rule applied on R2
```
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 8080 -j DNAT --to-destination 172.20.0.70:80
```

### Explanation
Traffic arriving at the router’s public IP on port 8080 is redirected to the internal web server at `172.20.0.70:80`.

### Validation
From the host machine:
```
curl http://PUBLIC_IP:8080
```

---

## 3. Firewall – Traffic Filtering on R2

### Allow only HTTP/HTTPS to LAN B
```
iptables -A FORWARD -p tcp -m multiport --dports 80,443 -j ACCEPT
```

### Block SSH from the Internet
```
iptables -A FORWARD -p tcp --dport 22 -j DROP
```

### Allow established/related traffic
```
iptables -A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT
```

### Explanation
- Only web traffic is allowed to reach the internal server.
- SSH access from the Internet is blocked for security.
- Responses to legitimate internal connections are allowed.

---

## 4. Diagnostic Tools

### tcpdump – Packet Capture
```
tcpdump -ni eth0 tcp port 8080
```
Used to verify that traffic reaches R2 and is forwarded correctly.

### curl – Service Testing
```
curl http://PUBLIC_IP:8080
```
Confirms that DNAT is functioning and the internal server is reachable.

### nmap – Port Scanning
```
nmap -p 22,80,443 PUBLIC_IP
```
Used to verify which ports are exposed externally.

### netstat / ss – Local Port Inspection
```
ss -tln
```
Shows which services are listening on the internal server.

---

## Conclusions
This lab demonstrates how to build a functional and secure border router using Docker and iptables:

- SNAT/PAT enables internal clients to access the Internet using a single public IP.
- DNAT allows publishing internal services to the outside world.
- Firewall rules enforce security by restricting and filtering traffic.
- Diagnostic tools validate and troubleshoot NAT and firewall behavior.

This setup mirrors real-world network edge configurations used in production environments.

---
