# Jellyfin Setup in a Dedicated LXC Container

To improve stability and performance, Jellyfin was separated from the main media stack. Running it alongside other services in the same VM caused frequent hangs due to resource limits.

---

## Configuration

| Parameter     | Value            |
|---------------|------------------|
| Type          | LXC Container    |
| OS            | Ubuntu LTS 22.04 |
| CPU           | 1 Core           |
| RAM           | 1 GB             |
| Storage       | 4 GB             |
| Storage Mount | SMB Share `/data` (same as media stack) |

---

## Setup Steps

### 1. Create LXC Container

- Download the Ubuntu 22.04 LTS template in Proxmox
- Create a new LXC container using that template with the above specs

### 2. Access the Container

```bash
pct enter <container_id>
apt update && apt upgrade -y
```

### 3. Mount SMB Share

Install CIFS utilities:
```bash
apt install cifs-utils
```
Create mount point and credential file:
```bash
mkdir /data
nano /etc/smb-credentials
```
Inside the credentials file:
```bash
username=your_smb_username
password=your_smb_password
```
Set permissions:
```bash
chmod 600 /etc/smb-credentials
```
Mount the SMB share:
```bash
mount -t cifs //nas_ip/share /data -o credentials=/etc/smb-credentials
```
To make it persistent, add this to /etc/fstab:
```bash
# Jellyfin media mount
//nas_ip/share /data cifs credentials=/etc/smb-credentials,iocharset=utf8,uid=1000,gid=1000,nounix,noserverino 0 0
```

### 4. Install Jellyfin

Run the official install script:
```bash
curl https://repo.jellyfin.org/install-debuntu.sh | bash
apt install jellyfin -y
```

### Access Jellyfin

Once the service is running, access the web dashboard at:
```bash
http://<lxc-ip>:8096
```
Configure your media libraries by pointing them to `/data/movies`, `/data/shows`, etc.
Jellyfin will now stream content directly from the SMB-mounted NAS storage.

## Notes

1.    No media is stored in the container itself

2.    All content is served over the SMB share

3.    You can reverse proxy this setup using Nginx, Traefik, or Cloudflare Tunnel