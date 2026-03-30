# LAB 06 – Security and TLS

## Objective

Demonstrate TLS, SSL termination, reverse proxy behavior, and basic secure communication principles.

---

## Architecture

Client → HTTPS → Nginx → HTTP → Backend

* Nginx acts as a reverse proxy
* TLS is terminated at Nginx
* Backend runs on plain HTTP

---

## Setup

### 1. Generate Self-Signed Certificate

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout key.pem \
-out cert.pem
```

---

### 2. Run Backend Server

```bash
python3 -m http.server 8081
```

---

### 3. Configure Nginx

```nginx
server {
    listen 80;
    server_name localhost;

    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name localhost;

    ssl_certificate /home/dayarojas/cert.pem;
    ssl_certificate_key /home/dayarojas/key.pem;

    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;

    location / {
        proxy_pass http://localhost:8081;
    }
}
```

---

### 4. Restart Nginx

```bash
sudo systemctl restart nginx
```

---

### 5. Test HTTPS

```bash
curl -k https://localhost
```

---

### 6. Test TLS Handshake

```bash
openssl s_client -connect localhost:443
```

---

## Key Concepts

### TLS Handshake

The client and server establish a secure session using asymmetric cryptography and negotiate encryption parameters.

---

### SSL Termination

Nginx handles TLS encryption and decrypts traffic before forwarding it to the backend over HTTP.

---

### Reverse Proxy

Nginx acts as an intermediary between the client and backend services.

---

### PFS (Perfect Forward Secrecy)

Using modern ciphers (ECDHE), session keys are ephemeral and cannot be reused if compromised.

---

### STARTTLS (Conceptual)

STARTTLS upgrades an existing plaintext connection to a secure one (used in SMTP, IMAP, etc.).

---

## Notes

* Self-signed certificates are used for demonstration purposes
* Private keys should never be committed to version control
