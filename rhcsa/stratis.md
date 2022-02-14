# Stratis 

- Stratis is a local storage-management solution for Linux. It is focused on simplicity and ease of use, and gives you access to advanced storage features.
- It uses Linux’s devicemapper subsystem and the XFS filesystem.
- The central concept of Stratis is a storage pool. This pool is created from one or more local disks or partitions, and volumes are created from the pool.
### The pool enables many useful features,
### such as:
- File system snapshots
- Thin provisioning
- Tiering


Component of stratis

```
File system      
                      ||fs1||  ||fs2||       ||fs1||  ||fs2||                  
Pool                    ||Pool 1||              ||  pool 2 ||   
                                                            
Block devices        /dev/sdb dev/sdc           dev/sdd dev/sde                         

```

## block devices
such as: disks ,partition
## Pool
- composed of one or more block devices
- size of pool is the sum of the size of all block devices
- startis creates a /dev/startis/my-pool/ directory for each pool. This directory contains link to devices in the pool.

## File System
- each pool can have one or more file systems
- the file system are formatted with XFS
- Startis creates a link to file system /dev/startis/my-pool/my-fs 



##  install stratis
```bash
# install stratis
yum install stratisd  stratis-cli
# check stratis running
systemctl status stratisd
# enable and start stratis
systemctl enable stratisd
systemctl start stratisd
# or
system enable --now stratisd 
```

## create pool
```bash
# create pool
stratis pool create my-pool /dev/sdb /dev/sdc
# check pool
stratis pool list
# expand pool
stratis pool add-data my-pool /dev/sdd
# list pool devices
stratis blockdev list 
```

## create file system
```bash
# create file system
stratis filesystem create my-pool my-fs
# check file system
stratis filesystem list
# mount file system
mount /startis/my-pool/my-fs /media
```
Add stratis to fstab
```bash
UUid=<uuid> stratis /media xfs defaults,X-systemd.requires=stratisd.service 0 0

# X-systemd.requires=stratisd.service >> The mount option delays mounting 
# the file system Systemd stratisd.service until after starts the during the boot process.
``` 
