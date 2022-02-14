# partition
list all partitions
using disk free space command 
```
df
df -h

```

list available disks
```
lsblk
```

sr0 for cdrom dvd ...etc
mount cd on it

# add new hard disk
on physical machine do restart to let new disk be recognized

on virtual machine do shutdown to let new disk be recognized


fdisk -l # list all connected storage

create partition
```
fdisk <disk>
fdisk /dev/sdb

```
let kernel know about new partition
"scanning all block devices"
```
partprobe  #scan all block devices
partprobe /dev/sdb #for one block 
```
create file system `mkfs command`
```
mkfs.ext4 /dev/sdb1
mkfs.xfs /dev/sdb1
```
xfs is faster than ext4


overwrite MBR of disk
```
cat /dev/random > /dev/sdb #but not recommended

dd if=/dev/zero of=/dev/sdb bs=512 count=1
```

next step is to mount partition
```
mount /dev/db1 /media/
```
to unmount
```
umount /media/
umount /dev/sdb1
```

use dumpe2fs to get all information about file system

dump extended 2 file system
```
dumpe2fs /dev/sdb1
```


check file system
cannot check when partition is mounted
```
e2fsck /dev/sdb1
e2fsck -f /dev/sdb1 #force check
```

take a backup of file system
```
dd if=/dev/sdb1 of=/dev/sdb1.bak
```


mount using block id
```
mount UUID=<id> /media/
```
get block id 
```
blkid 
blkid <partition>
```

give label to partition
```
e2label /dev/sdb1 <label>
```
mount using label
```
mount LABEL=<label> <mountPoint>
```
mount automatically 
using fstab

mount -a

cfdisk tool

```
cfdisk /dev/sdb
```

