# Replacing Google: Self-Hosted and Private Alternatives

This repo is based on one clear mindset:  
**No Google. No compromise.**

To match that theme, I’ve replaced two major Google services with fast, self-hosted, and open-source alternatives — both running inside **TrueNAS SCALE Apps** for simplicity and speed.

---

## Replacements

| Google Service     | Self-Hosted Alternative | Platform         |
|--------------------|-------------------------|------------------|
| Google Drive       | Nextcloud               | TrueNAS SCALE App |
| Google Photos      | Immich                  | TrueNAS SCALE App |

---

## Why TrueNAS SCALE Apps?

- One-click installs
- No need to manage Docker or command line
- Built-in update and rollback
- Automatic integration with storage pools and datasets

---

## 1. Nextcloud – Self-Hosted Google Drive

Nextcloud lets you store, sync, and share files just like Google Drive — but fully private and under your control.

### Setup Steps on TrueNAS SCALE:

1. Open the TrueNAS web UI
2. Go to **Apps → Available Applications**
3. Search for **Nextcloud**
4. Click **Install**
5. Configure:
   - Choose a name (e.g., `nextcloud`)
   - Set desired storage path (dataset or `/mnt/pool/nextcloud`)
   - Configure Ingress or NodePort for network access
   - Set admin user and password
6. Deploy and wait ~2 minutes

### Access:

- URL: `http://your-truenas-ip:<assigned_port>`
- Login with admin credentials
- Start uploading files, sync via mobile or desktop apps

---

## 2. Immich – Google Photos Replacement

Immich is a high-performance photo and video backup solution, focused on privacy and mobile-first experience. It auto-backs up your photos like Google Photos, but keeps everything local.

### Setup Steps on TrueNAS SCALE:

1. Open TrueNAS → **Apps → Available Applications**
2. Search for **Immich**
3. Click **Install**
4. Configure:
   - Choose name (e.g., `immich`)
   - Assign persistent storage paths for media and database
   - Set admin email and password
   - Configure Ingress or NodePort for external access
5. Deploy and wait for the app to initialize

### Access:

- URL: `http://your-truenas-ip:<assigned_port>`
- Login with email and password
- Install the **Immich Mobile App** and point it to your instance
- Enable auto-backup from your phone

---

## Final Thoughts

These two apps replaced 90% of what I used to rely on Google for. They are:

- **Open-source**
- **Private**
- **Under your control**
- **Easier to self-host than most people think**

---

## Optional: Secure Access

To access both apps remotely:

- Use **DuckDNS + NGINX reverse proxy** (see `nginx.md`)
- Enable HTTPS with free **Let's Encrypt certificates**
- Or tunnel everything with **Tailscale**

---

