# grub bootloader


mbr - partition table
    - bootloader       > 1st  stage
    - magic number


second stage            >/boot

all bootloader file in /boot/
    - kernel vmlinuz & initramfs / initrd
    - bootloader grub

configuration file of grub2 on /boot/grub2/grub.cfg







///////////////////////
edit /etc/default/grub

edit /etc/syscofig/grub


```
grub2-mkconfig -o /boot/grub2/grub.cfg
```



## SELinux 
> it is security system for linux 
SELinux  is used to give a `label` to a file or a directory 
```
ls -lZ /etc/shadow
```
z = for selinux show the label (context) of file


# root password recovery

edit menu entry in grub2

after linux16 quit on config file enter rd.break

rd.break it is a command that will break the boot process

and then start

after it will give you a root access to machine without password

> kernel have a small fs like normal system

the real on is under /sysroot

but  /sysroot is read only we need to make it rw
```
mount -o remount,rw /sysroot
```
-o =options
-o remount,rw = remount the filesystem as read-write

change root to /sysroot
```
chroot /sysroot/
```
change root password
```
passwd

```
relable the shadow file .autorelable 
let CLinux know that the password has been changed
```
touch /.autorelabel
```

if u create a file with .autorelabel
under /
it will tell CLinux make sure when reboot  check all file  and relabel missing file 

after exit and reboot
or logout



# reinstall grub first stage


# set pass for grub2

# recover password for grub2 and root


# disable alt + ctrl + delete
 comment out the line in /etc/init/control-alt-delete.conf

 
on redhat 7 and above

let ctrl-alt-del.target -> /dev/null
> mask ctrl-alt-del.target 
```

it will create a new file in /etc/systemd/system/ctrl-alt-del.target it will point to /dev/null

if u unmask it it will be remove and systemd will look at file in /usr/lib/systemd/system/

systemctl mask ctrl-alt-del.target
```
if u edit on target file
```
systemctl daemon-reload
```
instead of ctrl-alt-del.target -> reboot.target


systemd | search 
        |
        - 1 --/etc/systemd
        - 2--/user/lib/systemd   

if systemd don't  see configuration file on etc it will look on user/lib/systemd

