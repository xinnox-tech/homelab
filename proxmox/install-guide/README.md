# Proxmox Installation Guide

This guide walks you through installing Proxmox VE from scratch and preparing the system for future homelab services.

## Requirements
- USB drive (8GB+)
- Proxmox ISO
- Keyboard + monitor
- Two drives for ZFS mirror (optional but recommended)


---


## 1. Download Proxmox
Download the latest ISO from the official website.

Flash it using **balenaEtcher**, **Rufus**, or **Ventoy**.


---


## 2. Install Proxmox VE
- Boot from USB
- Accept EULA
- Choose **ZFS RAID1 (Mirror)** for redundancy or the drive where OS will be if only one drive
- Set region
- Create `root` password
- Configure hostname + IP


---


## 3. Access Proxmox Dashboard
Open:
```
https://<server-ip>:8006
```
Login as `root`.


---


## 4. Enable No-Subscription Repo
Run on node:
```bash
sed -i 's/^deb/#deb/' /etc/apt/sources.list.d/pve-enterprise.list
echo "deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription" > /etc/apt/sources.list.d/pve-no-subscription.list
apt update && apt full-upgrade -y
```

Or can be done via GUI in 

---


## Done!
Your Proxmox system is installed, updated, and ready for future services.