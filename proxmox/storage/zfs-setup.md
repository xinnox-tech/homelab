# ZFS Storage Setup


This guide covers creating ZFS mirrors, datasets, snapshots, and best practices.


## Create Mirror Pool
```bash
zpool create storage mirror /dev/sda /dev/sdb
```


## Create Dataset
```bash
zfs create storage/media
```


## Enable Compression
```bash
zfs set compression=lz4 storage
```


## List Pools
```bash
zpool status
```