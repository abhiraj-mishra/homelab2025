# Hypervisor – Notes & Insights

This is a raw, behind-the-scenes doc to track real-world learnings, problems, and internal notes from running Proxmox VE in my homelab. This complements the README by focusing on issues, fixes, automation, and future direction.

---

## Personal Goals with This Setup

- Master hypervisor tech like Proxmox, XCP-ng, ESXi
- Understand virtualization, clustering, and live migrations
- Run everything in containers or VMs — no services directly on host
- Build a reliable homelab to self-host media, dev tools, backups, etc.
- Transition to infrastructure-as-code (Ansible, Terraform) in 2025
- Document every config and setup in GitHub repo (`homelab2025`)
- Learn and implement failover, high availability, and remote access security

---

## Problems Faced & Solutions

### 1. **LXC Console Not Connecting**
- **Issue:** Tried to open a container console — got `Input/output error (os error 5)`
- **Fix:** A `dtach` process was stuck.
    ```bash
    ps aux | grep dtach
    kill -9 <pid>
    ```

---

### 2. **Pi-hole/CT Lost Internet After Reboot**
- **Issue:** Containers had no DNS resolution after Proxmox reboot
- **Fix:** Manually edited `/etc/resolv.conf` inside container:
    ```bash
    echo "nameserver 1.1.1.1" > /etc/resolv.conf
    ```

---

### 3. **No Network Bridge Inside CT**
- **Issue:** LXC stuck at boot, no network after IP change or template clone
- **Fix:**
    ```bash
    nano /etc/network/interfaces
    ifdown vmbr0 && ifup vmbr0
    ```

---

### 4. **Containers Not Starting on Boot**
- **Fix:**
    - Set `Start at boot` from GUI
    - Adjust `Boot order` and `Start/Stop delay` if needed to avoid overload

---

### 5. **Incorrect Disk Usage Reporting**
- **GUI showed wrong disk percent** — especially in thin provisioned containers.
- **Fix:** Always check from inside the container:
    ```bash
    pct exec <id> -- df -h
    ```

---

### 6. **Backups Stored Locally by Mistake**
- **Problem:** Proxmox defaulted to `local` storage for backups.
- **Solution:** Mounted NFS from TrueNAS and redirected backup jobs there.

---

### 7. **High RAM Usage on Idle VM**
- **Issue:** VMs show ~90% RAM even when idle (e.g. Ubuntu/TrueNAS)
- **Root Cause:** Linux caches aggressively; not actual usage
- **Check:**
    ```bash
    free -h
    top / htop
    ```

---

## Logs & Automation (Optional but Recommended)

You can create a script that logs this every day into `logs/`:

```bash
#!/bin/bash
mkdir -p /root/homelab-logs/$(date +%F)
pveversion > /root/homelab-logs/$(date +%F)/version.txt
uptime > /root/homelab-logs/$(date +%F)/uptime.txt
smartctl -a /dev/sda > /root/homelab-logs/$(date +%F)/drive-health.txt
```

## Future Experiments / Plans

Add 2nd node and configure Proxmox cluster

Explore Ceph storage for HA setup

GPU passthrough for Jellyfin VM or container

Enable email alerting for backup failures and SMART errors

Test PCI passthrough for TrueNAS VM

Deploy NGINX reverse proxy + Cloudflare tunnel for remote HTTPS

Track uptime/downtime via custom Grafana dashboard

Replace manual setup with Ansible scripts

## Personal Rules for Hypervisor Layer
No third-party services directly on Proxmox host

Keep Proxmox clean — treat it like a hypervisor, not a server

Always test containers/VMs in clone before upgrading

Snapshot > upgrade > verify > backup – never the other way around