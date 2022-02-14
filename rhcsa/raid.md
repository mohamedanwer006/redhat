# RAID  Redundant Array of independent ( inexpensive ) disks

## Hardware RAID  (RAID Controller)
  - cache memory
  - battery

One machine can have multiple RAID controller. <br> Array made of multiple disks on the same controller.    


## Software RAID
## Raid level
### RAID 0  
- stripping 
- fast write  fast Read  
- multiple disk 1 or more
- total size sum of disks  
- not support disk failure

### RAID 1
 - mirroring
 - slow write fast read as it read from multiple disk
 - support disk fail
 - usable apace = small disk size
### RAID 5
 - striping with parity
 - minimum 3 disk 
 - one disk failure support
 - usable apace =   sum - 1 disk 

```
 disk1   disk2     disk3
|| a || || b || || Parity || 

=> parity checksum of a nd b  = XOR

```
### RAID 6
- stripping with dual distributed parity
- 2 disk failure support
- use even disks
- minimum 4 disk
- usable apace  = sum - 2 disk 
```
 disk1   disk2     disk3        disk4     
|| a || || b || || Parity || || Parity2 ||

=> parity checksum of a nd b  = XOR

```

### RAID 10
 - RAID1 + RAID0
 - mirroring + stripping
 - even disks
 - minimum 4 disk
 - usable apace  = 1/2 sum
```
                 RAID 0
         ______________________                                    
        |                     |          
 || d1 || d2 ||          ||d3 || d4 ||
|______________|       |______________|                              
      RAID 1                RAID 1
```



## RAID device 
### Represent a set of disks that are used to store data.
>Implementation o software RAID  `  mdadm  ` multiple disk admin 



create raid device
```bash
mdadm --create /dev/md0 --level=5 --raid-devices=3 /dev/sdb /dev/sdc /dev/sdd
```
get status of raid device
```bash
cat /proc/mdstat
# or
mdadm --detail /dev/md0
```

make fs on raid device
```bash

mkfs.xfs /dev/md0
```
add new disk to raid device
```
mdadm --add /dev/md0 /dev/sdd
```
stop raid 
```
mdadm --stop /dev/md0
```

assemble raid device
```
mdadm --assemble /dev/md0 /dev/sdb /dev/sdc /dev/sdd
mdadm --assemble --scan

```

remove raid (super block) , can't assemble again
```
mdadm --zero-superblock /dev/sdb
mdadm --zero-superblock /dev/sdc
mdadm --zero-superblock /dev/sdd
```


# raid on partition

- create partition
- change partition system id to raid



faulty disk (disk fail)
```
mdadm /dev/md0 -f /dev/sdb
mdadm /dev/md0 --fail /dev/sdb
```





