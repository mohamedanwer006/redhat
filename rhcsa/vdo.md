# VDO

Virtual data optimizer 

Data deduplicate and optimizes data storage by using a virtual data object (VDO) to store data.

## Install vdo 
```
yum install vdo
```
### Enable vdo services 
```
systemctl enable vdo
systemctl start vdo
systemctl status vdo.service

```
>it's enable and installed by default in redhat 8



### Use of vdo 
```
vdo create --name=my-vdo --device=/dev/sdb --vdoLogicalSize=20G --verbose
```


### Create fs on vdo
```
mkfs.xfs -K /dev/mapper/my-vdo
```
### Mount vdo
```
mount /dev/mapper/my-vdo /my-vdo
```

`systemctl restart vdo.service`

### Permanent mount on /etc/fstab
```bash
# vim /etc/fstab add below line
/dev/mapper/my-vdo /my-vdo xfs defaults,x-systemd.requires=vdo.service 0 0
# require vdo.service to mount
# x-systemd.requires=vdo.service 
# check mount
mount -a
```

### Get vdo status
```
vdo status --human-readable
```
