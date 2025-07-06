# 🧠 DIY TrueNAS Build – Cheap, Powerful & Custom NAS at Home

![TrueNAS Dashboard]((../../assets/screenshots/truenas.png))

---

## 🧊 What is NAS?

**NAS (Network Attached Storage)** is basically your personal Google Drive — but local, faster, and fully in your control.

You attach a few drives in **RAID config**, create **NFS/SMB shares**, and boom — all devices in your network can access it like magic.

---

## 🛠️ Building a NAS: 2 Simple Steps

### 1. Hardware Choice

You have two options:
- 💸 **Buy an off-the-shelf NAS**:  
  - 2-bay = ₹25K+  
  - 4-bay = ₹35K+

- 🧠 **Build your own NAS** using old PC parts (much cheaper):  
  - DIY 4-bay NAS = ₹0–₹20K depending on your spare parts

**My Build:**
- 💻 Base: Old HP SFF machine
- 💾 Drives: 2 × 500GB HDD in **RAID 1 (Mirror Mode)**  
  → If one fails, data still safe. No panic.

---

### 2. Software Choice

You can either:
- Use **Windows with shared folders** (not recommended)
- OR go pro with a **dedicated NAS OS**:

| OS             | Cost     | Features                              |
|----------------|----------|---------------------------------------|
| OpenMediaVault | Free     | Simple, beginner friendly             |
| TrueNAS        | Free     | Feature-rich, more technical          |
| Unraid         | Paid 💰  | Super flexible, but paywall exists    |

### 👉 I Chose: **TrueNAS**
Even though OpenMediaVault is easier, I went with TrueNAS...  
Because let’s be honest — **tech is fun** 😎

---

## 💻 My TrueNAS VM Specs

| Resource | Value        |
|----------|--------------|
| CPU      | 2 Cores      |
| RAM      | 4 GB *(more = better)* |
| SSD      | 64 GB *(32 GB is enough, I overdid it)* |

> ⚠️ Tip: Add more RAM if using ZFS — it improves caching & write speed big time.

---

## 🔧 TrueNAS Installation (Super Easy)

🔗 **Video Tutorial**: [How to Install TrueNAS](https://youtu.be/M3pKprTdNqQ?si=Mkynyi2kmhUSb9EK)

### Steps:

1. **Download** ISO from [TrueNAS Website](https://www.truenas.com/download/)
2. In Proxmox or your hypervisor, go to local (your-node-name) → Upload ISO
3. **Create a new VM** and boot using the ISO
4. Follow the on-screen instructions
5. After install, you’ll see a **dedicated IP**
6. Open browser *(anything but Google pls)* →  
`http://<your-truenas-ip>`
7. **Login** with:
- **Username**: `truenas_admin`
- **Password**: the one you set

🎉 **Boom — you’re in.**

---

## 🔒 Coming Next:

I'll show you:
- How to set a **static IP** so your NAS doesn't break after a reboot or DHCP reset
- Add SMB/NFS shares
- Setup automatic snapshots & ZFS tricks

---

## 📌 TL;DR

> **Build your own NAS** with old hardware + TrueNAS  
> It’s powerful, cheaper than branded options, and fun to build.

---

