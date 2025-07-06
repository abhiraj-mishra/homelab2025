
# Homepage Dashboard – Centralized Control for Homelab

This is a self-hosted, beautiful, and customizable **start page dashboard** to monitor and access all your services from one place. It uses `gethomepage.dev`, a modern dashboard framework with YAML config.

![Dashboard Preview](../assets/screenshots/dashboard.png)

---

## 🚀 Features

- Centralized homepage for all homelab services
- Service monitoring (site status, CPU/RAM, uptime)
- Auto-updated widgets (weather, RSS, crypto, etc.)
- Fully YAML-based configuration
- Supports Docker labels and Portainer integration
- Secure access (optional via reverse proxy or VPN)

---

## 📦 File Structure

| File                 | Purpose                            |
|----------------------|------------------------------------|
| `.env`               | Environment variables (used in Docker) |
| `docker-compose.yaml`| Docker setup for the dashboard     |
| `services.yml`       | Service tiles + links              |
| `settings.yml`       | App-wide settings & appearance     |
| `widgets.yml`        | Weather, clocks, search bar, etc.  |
| `readme.md`          | You're reading it 👀               |

---

## 🐳 Running It (Docker)

> Make sure Docker + Docker Compose is installed.

1. Clone this repo:
   ```bash
   git clone https://github.com/yourname/homelab-dashboard.git
   cd homelab-dashboard/06_homepage
   ```

2. Start the container:
   ```bash
   docker-compose up -d
   ```

3. Access the dashboard at:
   ```
   http://<your-ip>:3000
   ```

---

## 🧩 Configuration

### 🔧 `settings.yml`

Controls global UI options:

- Theme
- Icon packs
- Layout styles (grid, column, row)
- Title/logo

### 🧭 `services.yml`

This is where you define:

- Categories (e.g., Hypervisor, Networking, Media)
- Services with:
  - Icon
  - URL
  - Status monitor
  - Custom widget (e.g., Proxmox, Sonarr)

### 📊 `widgets.yml`

Adds optional widgets like:

- Weather
- Time zones
- Search bar
- System stats (with Glances)
- UptimeRobot integration

---

## 🔐 Security (Optional)

- Expose this only via **VPN**, **Tailscale**, or behind **NGINX with auth**
- Use Docker secrets or `.env` for credentials

---

## 🧠 Tips

- Icons are pulled from [https://github.com/walkxcode/dashboard-icons](https://github.com/walkxcode/dashboard-icons)
- To add CPU/RAM usage widgets, integrate with Glances:
   ```bash
   docker run -d      --name glances      -p 61208-61209:61208-61209      --restart unless-stopped      --pid host      -v /var/run/docker.sock:/var/run/docker.sock:ro      nicolargo/glances:latest-full
   ```
- Point widgets to Glances IP in `widgets.yml`

---

## 📸 Screenshot

> ![Dashboard Screenshot](../assets/screenshots/dashboard.png)

---

## ✅ Done!

Now you’ve got a beautiful, lightweight dashboard running to monitor and launch all your services from a single place. Simple to use. Easy to extend.

---
