# Setting a Static IP in TrueNAS

To ensure your NAS is always reachable at the same address, it’s important to assign it a static IP. This avoids issues caused by dynamic DHCP-assigned IPs changing after reboots.

## Method 1: Via Web UI

1. **Log in to the TrueNAS web dashboard.**
2. Navigate to:  
   `Network` → `Interfaces`
3. Click **Edit** on the interface you want to assign a static IP to.
4. In the **IPv4 Configuration Type**, select `Static`.
5. Enter the desired IP address and subnet mask (e.g., `192.168.1.100/24`).
6. Optionally, add a default gateway and DNS servers under:  
   `Network` → `Global Configuration`
7. Click **Save**, then **Apply Changes**.
8. Reboot to verify the IP remains persistent.

## Method 2: During Installation

If you prefer setting the IP during initial setup:

- Use the CLI setup menu during install to assign a static IP manually.
- You can later change it in the UI if needed.

---

