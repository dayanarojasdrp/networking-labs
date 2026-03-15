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

