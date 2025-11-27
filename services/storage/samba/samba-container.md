# Samba LXC Container Guide


This LXC provides network-attached storage for future services.


## Create Container

### Option 1:
- Debian 12 template   ( or prefer one)
- 2 vCPU / 2GB RAM
- Unprivileged
- Mount dataset → `/mnt/storage`


## Install Samba
```bash
apt update
apt install samba -y
```


## Configure Share
Edit `/etc/samba/smb.conf`.
```
[BulkStorage]
path = /mnt/storage/share
read only = no
guest ok = yes
```

