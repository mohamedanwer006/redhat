know inode number
```
ls -i <fileName>
ls -li <fileName>
```
know available partition

disk free space
```
df
#human readable
df -h
#inode
df -i
```
soft link = shortcut on windows
```
ln -s <source> <target>
``` 
hard link  
```
ln <source> <target>
```
 
list block devices
```
lsblk
```



list disks
```
fdisk -l

```
create partition
```
fdisk <device>
```
make kernel aware of partition table (reread partition table)
```
#reread for all disks
partprobe
#reread for specific disk
partprobe <device>
#for example
partprobe /dev/sdb
```
create file system
```
mkfs
```

over writer partition table
```
cat /dev/random >> /dev/sdb

dd if=/dev/random of=/dev/sdb count=512
``` 
```
dd if=/dev/zero of=/dev/sdb bs=512 count=512
```
mount partition
```
mount <device> <mountPoint>
for example
mount /dev/sdb1 /media/sdb1
#mount using uuid
mount UUID=<uuid> <mountPoint>
```
unmount partition
```
umount <mountPoint>
unmount <device>
unmount UUID=<uuid>
```
give partition a label
```
e2label <device> <label>
```

get info about  partition
```
dumpe2fs <device>
dumpe2fs /dev/sda1
``` 
dumpe2fs (dump ext2 file system) works only on ext2/3/4

check partition
```
e2fsck <device>
e2fsck /dev/sdb1
#force check
e2fsck -f <device>
```
## **hint** before force check make sure that partition is not mount and ,take a backup of partition

backup partition using dd 

```
dd if=/dev/sdb1 of=/dev/sdb1.bak
```
to restore backup
```
dd if=/dev/sdb1.bak of=/dev/sdb1
```
dd = disk dump or data dump or disk destroyer



cfdisk tool to create partition table
```
cfdisk <device>
```