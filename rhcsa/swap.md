# SWAP

Create a new partition on the disk.

```bash
fdisk /dev/sdb
# press n for new partition
# press  t for partition label 
# set to swap 
# press w to write
partprobe /dev/sdb
blkid /dev/sdb1
# copy UUID from blkid
vim /etc/fstab 
# Add UUID=<uuid> swap swap defaults 0 0
#check fstab mount
mount -a

```