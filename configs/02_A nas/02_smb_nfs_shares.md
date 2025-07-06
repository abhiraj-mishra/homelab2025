# Configuring SMB and NFS Shares in TrueNAS

TrueNAS allows file sharing over multiple protocols including SMB (Windows/macOS) and NFS (Linux/Unix). Here's how to set up each.

## SMB Share (for Windows/macOS)

1. Go to:  
   `Storage` → `Pools` → Create a dataset for sharing (optional but recommended).
2. Navigate to:  
   `Sharing` → `Windows (SMB)` → Add
3. Fill in:
   - Path: Select the dataset/folder
   - Name: Share name
4. Enable access control under `ACL` to configure who can read/write.
5. Enable the SMB service under:  
   `Services` → Start and enable **SMB**
6. Access the share from other devices using:  
   `\\<your-nas-ip>\<sharename>`

## NFS Share (for Linux/Unix)

1. Go to:  
   `Sharing` → `Unix (NFS)` → Add
2. Fill in:
   - Path: Select dataset/folder
   - Authorized Networks: E.g., `192.168.1.0/24`
3. Set permissions to allow read/write as needed.
4. Enable the NFS service under:  
   `Services` → Start and enable **NFS**
5. Mount the share on client systems using:
   ```bash
   sudo mount -t nfs <your-nas-ip>:/mnt/<pool>/<dataset> /mnt/your_mount_point
