# Reverse Proxy Setup with NGINX + DuckDNS + SSL (Inside Docker in LXC)

This guide explains how to deploy an NGINX reverse proxy with HTTPS certificates using **DuckDNS** and **Let's Encrypt**, all inside a Docker container running in an **LXC** on Proxmox.

---

## System Overview

| Component | Role                          |
|----------|-------------------------------|
| LXC       | Container to run Docker       |
| Docker    | Containerized service runtime |
| NGINX     | Reverse proxy + HTTPS support |
| DuckDNS   | Dynamic DNS for home IP       |
| Certbot   | Auto-renews free SSL certs    |

---

## 1. Setup LXC Container for Docker

Create a privileged LXC container (or unprivileged with nesting + fuse):

- OS: Ubuntu LTS 22.04
- Resources: 1 CPU / 1–2 GB RAM / 4–8 GB storage
- Enable:
  - `features: nesting=1`
  - `features: keyctl=1`
  - `features: fuse=1`

Inside container:

```bash
apt update && apt upgrade -y
apt install docker.io docker-compose -y

## 2. Setup DuckDNS

    Register at `https://duckdns.org`

    Create a subdomain (e.g., `yourname.duckdns.org`)

    Copy your token


## 3. Setup Directory Structure

Create the working directory:
```bash
mkdir -p ~/nginx-reverse-proxy && cd ~/nginx-reverse-proxy
```

## 4. Create .env File
```bash
DOMAIN=yourname.duckdns.org
EMAIL=you@example.com
DUCKDNS_TOKEN=your_duckdns_token
```

## 5. Create Docker Compose File

File: `docker-compose.yml`
```bash
version: '3'

services:
  nginx:
    image: nginx:latest
    container_name: nginx-reverse-proxy
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - ./certs:/etc/letsencrypt
      - ./html:/usr/share/nginx/html
    restart: unless-stopped

  certbot:
    image: certbot/certbot
    container_name: certbot
    volumes:
      - ./certs:/etc/letsencrypt
    entrypoint: /bin/sh -c
    command: >
      "certbot certonly --standalone --preferred-challenges http
       --agree-tos --no-eff-email --email $EMAIL
       -d $DOMAIN --non-interactive && touch /certs/ssl.done"
```

## 6. Create nginx.conf

File: `nginx.conf`
```bash
events {}

http {
  server {
    listen 80;
    server_name ${DOMAIN};

    location / {
      return 301 https://$host$request_uri;
    }
  }

  server {
    listen 443 ssl;
    server_name ${DOMAIN};

    ssl_certificate /etc/letsencrypt/live/${DOMAIN}/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/${DOMAIN}/privkey.pem;

    location / {
      proxy_pass http://your_internal_ip:your_service_port;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
    }
  }
}
```

## 7. Issue SSL Certificate

Once `.env` and `docker-compose.yml` are set:
```bash
docker-compose run certbot
```
Make sure port 80 is open for this to succeed.


## 8. Launch NGINX with SSL

Once the cert is successfully generated:
```bash
docker-compose up -d nginx
```
Test it by going to:
`https://yourname.duckdns.org`


## 9. Set Up Auto-Renewal (Optional)

You can add a cron job to renew SSL every 60 days:
```bash
crontab -e
```
Add:
```bash
0 3 * * 1 docker-compose run certbot renew --quiet
```


## Notes

    You can reverse proxy multiple services by editing `nginx.conf`

    Always expose services over HTTPS when accessible from the internet

    To reverse proxy Jellyfin or Portainer, use their internal IP and port in `proxy_pass`