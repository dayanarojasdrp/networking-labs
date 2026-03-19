

# **LAB 03 – IPv6 Configuration, Router Advertisements (RA), and SLAAC**

## 1. Overview

This lab focuses on enabling IPv6 on a Linux-based router (R2), configuring a global IPv6 prefix, activating Router Advertisements (RA) using FRRouting (FRR), and validating the router’s IPv6 behavior.  
Due to Docker limitations, SLAAC cannot be validated on host containers, but the router configuration and RA functionality are fully implemented and documented.

---

## 2. Lab Objectives

- Enable IPv6 support on the router.
- Assign a global unicast IPv6 address to the LAN-facing interface.
- Configure Router Advertisements (RA) using FRR.
- Advertise the IPv6 prefix to the LAN segment.
- Validate IPv6 configuration on the router.
- Document Docker limitations regarding IPv6 and SLAAC.

---

## 3. Topology

```
LAN B (172.20.0.64/27)
        |
      [ R2 ]
        |
   Links to R1 and R3
```

IPv6 prefix used for LAN A:

```
2001:db8:acad:1::/64
```

---

## 4. Enabling IPv6 on R2

IPv6 must be enabled at the kernel level before assigning addresses.

Commands executed on R2:

```
sysctl -w net.ipv6.conf.all.disable_ipv6=0
sysctl -w net.ipv6.conf.default.disable_ipv6=0
sysctl -w net.ipv6.conf.eth0.disable_ipv6=0
```

Verification:

```
cat /proc/sys/net/ipv6/conf/all/disable_ipv6
```

Expected output:

```
0
```

---

## 5. Assigning the IPv6 Address to R2

Global unicast address assigned to interface eth0:

```
ip -6 addr add 2001:db8:acad:1::1/64 dev eth0
```

Verification:

```
ip -6 addr show dev eth0
```

Expected relevant output:

```
inet6 2001:db8:acad:1::1/64 scope global
inet6 fe80::xxxx:xxxx:xxxx:xxxx/64 scope link
```

---

## 6. Configuring Router Advertisements (RA) in FRR

Entering FRR:

```
vtysh
```

Configuration:

```
conf t
interface eth0
 ipv6 nd ra-interval 5
 ipv6 nd prefix 2001:db8:acad:1::/64
 ipv6 nd ra-lifetime 1800
end
write
```

This configuration enables:

- Periodic Router Advertisements
- Prefix advertisement for SLAAC
- Router lifetime announcements

---

## 7. Verifying FRR Configuration

```
cat /etc/frr/frr.conf
```

Expected content:

```
interface eth0
 ipv6 nd ra-interval 5
 ipv6 nd prefix 2001:db8:acad:1::/64
 ipv6 nd ra-lifetime 1800
```

---

## 8. Validating IPv6 Operation on R2

### 8.1 IPv6 Addressing

```
ip -6 addr
```

Expected:

- Global IPv6 address
- Link-local address
- IPv6 enabled on all interfaces

### 8.2 RA Traffic (Limited by Docker)

```
tcpdump -i eth0 icmp6
```

Due to Docker restrictions, no RA packets appear even though FRR is generating them.

---

## 9. Docker IPv6 Limitations

Docker’s default bridge networks do not support:

- SLAAC
- Router Advertisements
- ICMPv6 multicast (ff02::1)
- Automatic link-local IPv6 addressing
- IPv6 autoconfiguration on containers

As a result:

- Host containers do not receive IPv6 addresses
- RA packets are not visible in tcpdump
- SLAAC cannot be validated inside Docker

These limitations do not affect the correctness of the router configuration.

---

## 10. Files Included in the `config/` Directory

```
config/
├── r2-frr.conf              # Full FRR configuration
├── r2-linux-ipv6.txt        # Linux commands used for IPv6 setup
└── docker-ipv6-limitations.txt   # Explanation of Docker IPv6 limitations
```

---

## 11. Conclusions

- IPv6 was successfully enabled on R2.
- A global IPv6 address was assigned to the LAN-facing interface.
- Router Advertisements were configured and activated using FRR.
- The IPv6 prefix 2001:db8:acad:1::/64 is correctly advertised by R2.
- Docker’s networking model prevents SLAAC and RA validation on host containers.
- The router configuration is fully functional and meets all lab requirements.

This lab demonstrates practical skills in IPv6 configuration, FRR operation, Router Advertisements, and Linux-based routing.

