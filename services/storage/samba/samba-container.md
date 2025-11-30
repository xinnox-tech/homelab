# Samba LXC Container Guide


This LXC provides network-attached storage for future services.


## Create LXC

- Ubuntu 24 template   ( or prefer one)
- 2 vCPU / 2GB RAM ( or more if needed )
- Unprivileged
- Mount dataset → `/mnt/storage`


## Update LXC
```
apt update && apt upgrade -y
```

## Add User
```
adduser [username]
adduser [username] sudo
```

## Switch User
```
sudo su - [username]
```

## Set permissions
```
sudo chown -R [username]:[username] /share
```

## Install Samba
```
sudo apt install samba -y
```

## Configure Share
Can either make a backup and create a new one, or rewrite the one thats there.

### Create Copy
```
cd /etc/samba
sudo mv smb.conf smb.conf.bk
```

### Replace/Edit
Edit `/etc/samba/smb.conf`.
Using `sudo nano smb.conf`

Replace everything with:
```
[global]
    server string = Samba
    workgroup = WORKGROUP
    security = user
    map to guest = Bad User
    name resolve order = bcast host
    hosts allow = 192.168.1.0/24
    hosts deny = 0.0.0.0/0

[storage]
    path = /mnt/storage/share
    force user = xinnox
    force group = xinnox
    create mask = 0774
    force create mode = 0774
    directory mask = 0775
    force directory mode = 0775
    browseable = yes
    writable = yes
    read only = no
    guest ok = no
```

## Add your samba user
```
smbpasswd -a [username]
```
## Set services to auto start on reboot
```
sudo systemctl enable smbd
sudo systemctl restart smbd
```

## Install wsdd for Windows
```
sudo apt install wsdd
sudo apt install wsdd-server
```

## Allow services on firewall (if run into issues.)
```
sudo  allow OpenSSH
sudo ufw allow Samba
# following 3 are needed for wsdd
sudo ufw allow 3702/udp
sudo ufw allow 5357/tcp
sudo ufw allow 5358/tcp
# Check ufw status
sudo ufw status
```

