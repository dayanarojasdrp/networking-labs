## IP address assignment per router

### Router R1
| Interfaz | Red | IP |
|----------|------|------|
| R1-LAN-A | LAN A | 10.10.0.1/26 |
| R1-R2    | Enlace R1–R2 | 10.10.0.113/30 |

### Router R2
| Interfaz | Red | IP |
|----------|------|------|
| R2-R1 | Enlace R1–R2 | 10.10.0.114/30 |
| R2-R3 | Enlace R2–R3 | 10.10.0.117/30 |

### Router R3
| Interfaz | Red | IP |
|----------|------|------|
| R3-R2    | Enlace R2–R3 | 10.10.0.118/30 |
| R3-LAN-B | LAN B | 10.10.0.65/27 |
| R3-LAN-C | LAN C | 10.10.0.97/28 |
