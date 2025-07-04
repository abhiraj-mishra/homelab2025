# 🏡 homelab2025

Hi, I’m Abhiraj — building and documenting my self-hosted homelab journey.  
From zero to full-stack infra, powered by Proxmox, TrueNAS, Docker, and open-source sauce.

> This repo = my configs, learnings, automations, mistakes, and glow-ups.

---

## 📦 Stack Snapshot

| Category     | Tools |
|-------------|-------|
| 🧠 Hypervisor  | Proxmox VE |
| 💾 Storage     | TrueNAS SCALE |
| 🌐 Network     | Pi-hole, OPNsense (placeholder) |
| 📺 Media Stack | Jellyfin, Sonarr, Radarr, Prowlarr, qBittorrent |
| 🐳 Containers  | Portainer, Docker Compose |
| 💻 Dev & Code  | GitHub, GitLab |

---

## 🔧 What’s Inside

- `/configs` – All my `.yaml`, `.env`, and service configs
- `/docs` – Learnings, diagrams, mistakes, and plans
- `/scripts` – Automation (cron, bash, update scripts)
- `/assets` – Screenshots and diagrams
- `/README.md` – This file you’re reading 👀

---

## 📸 Live Setup Preview

> Main dashboard (Homepage container UI)

![Dashboard Preview](assets/screenshots/dashboard.png)

---

## 🗃️ Example Projects in the Lab

- 🧰 `proxmox` – Node setup, auto shutdown, VM templates
- 💽 `truenas` – NAS config, caching, pool layout
- 🚀 `docker` – Jellyfin, qBittorrent, Homepage, etc.
- 🧱 `infra` – Static IPs, firewall setup, DNS routing
- ☁️ `backup` – 3-2-1 with local + cloud (planned)

---

## 🧠 Lessons So Far

- 💡 Avoid putting passwords in `.yaml` — use `.env` + `.gitignore`
- 🔐 Reverse proxy + fail2ban = essential if you go public
- 📉 Self-hosting eats RAM fast — monitor with Grafana/Netdata
- 🧼 Cleanup scripts & automation will save your sanity

---

## 🛣️ Roadmap

- [ ] Nginx reverse proxy w/ SSL
- [ ] Alerting system (Uptime Kuma + Email)
- [ ] Second Proxmox node (Optiplex 3060)
- [ ] Cloud backup automation (S3 / Rclone)
- [ ] Publish dashboard via GitHub Pages

---

## ⚙️ Getting Started

1. Clone the repo
2. Head into `configs/`
3. Adjust `.env` and `docker-compose.yaml` for your setup
4. Start container stack → `docker compose up -d`
5. Done.

---

## 🤝 Contributions

This is my personal lab but if you’re on the same grind — open an issue, drop a PR, or start a discussion.

---

## 📜 License

MIT License. Use anything you like, just don’t blame me if it breaks 😉

---

> Homelab = digital playground + life skills unlocked.  
> Cheers from 🌐 India.
