
# **iptables Rules – NAT, Firewall and Diagnostics**

## 1. SNAT / PAT – Internet Access for Internal Hosts
```bash
iptables -t nat -A POSTROUTING -s 172.20.0.0/26 -o eth0 -j MASQUERADE
```

**Explanation:**  
This rule enables internal hosts in LAN A to access the Internet using the router’s public IP.  
`MASQUERADE` performs dynamic SNAT/PAT, allowing multiple clients to share a single external address.

---

## 2. DNAT – Publishing an Internal Web Server
```bash
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 8080 -j DNAT --to-destination 172.20.0.70:80
```

**Explanation:**  
Traffic arriving at the router on port 8080 is redirected to the internal web server located in LAN B at `172.20.0.70:80`.

---

## 3. Firewall Filtering Rules
```bash
iptables -A FORWARD -p tcp -m multiport --dports 80,443 -j ACCEPT
```
**Explanation:**  
Allows only HTTP and HTTPS traffic to reach the internal server.

```bash
iptables -A FORWARD -p tcp --dport 22 -j DROP
```
**Explanation:**  
Blocks SSH access from the external network for security.

```bash
iptables -A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT
```
**Explanation:**  
Allows return traffic for already established connections.

---

## 4. Optional Default Policy
```bash
# iptables -P FORWARD DROP
```

**Explanation:**  
This optional rule enforces a default deny policy, dropping any forwarded traffic not explicitly allowed.

---

## 5. Diagnostic Tools Used
- **tcpdump** to capture and inspect traffic on external and internal interfaces.  
- **curl** to validate DNAT and service reachability.  
- **nmap** to verify open/filtered ports from the external network.  
- **ss / netstat** to confirm listening services inside containers.
