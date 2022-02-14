# LVM STORAGE
Logical Volume Manager (LVM) is a tool for managing storage volumes.

```
physical disk (partition) -> physical volume (pv) -> volume group (vg) -> logical volume (lv)
||||||| => extents 
|||||||
logical volume 
default extents size = 4M
```

allocate partition size that is divisible by the size of extent


create physical volume
```bash
pvcreate /dev/sdb /dev/sdc1
#scan all physical volume
pvs
#display all physical volume
pvdisplay
#remove physical volume
pvremove /dev/sdb /dev/sdc1

```
create volume group
```bash
vgcreate data /dev/sdb /dev/sdc1
#scan all volume group
vgs
#display all volume group
vgdisplay 
#remove vg
vgremove data

```
create logical volume
```bash
lvcreate --size 25G --name redhat data
#scan all logical volume
lvs
#display all logical volume
lvdisplay
#remove lv
lvremove /dev/data/redhat

```
will create soft link on /dev/data/redhat 
to device mapper


# lvm extend 

```bash
# extend logical volume 
# don't need to umount volume
lvextend --size +5G /dev/data/redhat
# update inode table
resize2fs /dev/data/redhat
# for xfs formatting
xfs_growfs /dev/data/redhat
```

# lvm shrink
```
# first check fs
e2fsck -f /dev/data/redhat
# update inode table
resize2fs /dev/data/redhat 25G
# shrink logical volume
lvreduce --size -5G /dev/data/redhat
```

> By default lvm write data to disks linearly



# lvm stripping high I\O
number of disk to write data to
```bash

lvcreate --size 25G --name redhat --stripes 2 data
# check stripe
dmsetup deps /dev/data/redhat

```
# lvm mirroring
# lvm snapshot
- Take image of volume (snapshot)  
- COW (copy on write)
`revert`or `merge`

```bash
lvcreate --size 25G --name redhat-snapshot --snapshot /dev/data/redhat
```

> umount volume

```bash
lvconvert --merge /dev/data/redhat-snapshot
# extend snapshot
lvextend --size +5G /dev/data/redhat-snapshot
# automatic resize snapshot
# vim /etc/lvm/lvm.conf
# search snapshot 
# modify snapshot_autoextend_threshold = 100 to 
# snapshot_autoextend_threshold = 80 
```

 


# lvm thinpool
