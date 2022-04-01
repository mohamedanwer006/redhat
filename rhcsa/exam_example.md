# Exam

## Exam environment at [rdbreak](https://github.com/rdbreak/rhce8env)

Ensure all the tasks are implemented with firewalld and SELinux enabled. Your server
should be able to survive a reboot. Good luck!

-------

## Systems Set Up
### Hostname - system1.eight.example.com
1. IP - 192.168.55.150/24
2. DNS - 8.8.8.8
3. GW - 192.168.5.1
### Hostname - system2.eight.example.com
1. IP - 192.168.55.151/24
2. DNS - 8.8.8.8
3. GW - 192.168.5.1


1. 15GB disk space with LVM partitions.
     a. 10GB - /
     b. 1GB - swap
     c. 1GB - boot
     d. 4GB - unallocated space
2. If you're using a custom environment, then add an additional 5GB disk for use in
    the exam. If you're using the automated deployment, then an additional disk is
    already supplied for you to use.
NOTE - The below questions assume you're using the automated deployment but you can
also use a practice environment you created. However, you will have to set up your own
repo, change host names, IP addresses, etc to reflect your own environment details.

-------

1. Interrupt the boot process and reset the root password. Change it to "wander" to
  gain access to the system.

```bash
# restart the system
# press `e` to edit 
# find the line start with linux press `end` to go to the end of the line
# add the following
rd.break enforcing=0
# press ctrl+x to save and exit
mount -o remount,rw /sysroot

chroot /sysroot
passwd
exit
exit
restorecon /sysroot
setenforce 1

# restart to check

## or 
##
rd.break
mount -o remount,rw /sysroot
chroot /sysroot
passwd
touch /.autorelabel
exit
exit
```

1. Repos are available from the repo server at http://repozeight.example.com/BaseOS and http://repo.eight.example.com/AppStream for you to use during the exam.

```bash
vim /etc/yum.repos.d/BaseOS.repo
#### add the following lines
[BaseOS]
name=BaseOS
baseurl=http://repo.eight.example.com/BaseOS
enabled=1
gpgcheck=0
[AppStream]
name=AppStream
baseurl=http://repo.eight.example.com/AppStream
enabled=1
gpgcheck=0

## or using dnf
dnf config-manager --add-repo http://repo.eight.example.com/BaseOS
dnf config-manager --add-repo http://repo.eight.example.com/AppStream

## check
dnf repolist

```  
3. The system time should be set to your (or nearest to you) timezone and ensure
   NTP sync is configured.

```bash
timedatectl set-timezone Africa/Cairo
timedatectl set-ntp yes

systemctl status chronyd
## if not running
systemctl enable --now chronyd

``` 
4. Add the following secondary IP addresses statically to your current running
   interface. Do this in a way that doesn't compromise your existing settings:
     a. IPV4 - 10.0.0.5/24
     b. IPV6 - fd01::100/64
```bash
nmcli conn mod eth1 +ipv4.address 10.0.0.05/24
nmcli conn reload
nmcli conn mod eth +ipv6.address fd01::100/64
nmcli conn reload

```      
5. Enable packet forwarding on system1. This should persist after reboot.
```bash
vim /etc/sysctl.conf

cat /proc/sys/net/ipv4/
reboot
cat /proc/sys/net/ipv4/

# add the following line
net.ipv4.ip_forward=1

``` 
6. System1 should boot into the multi-user target by default and boot messages should be present (not silenced).

```bash
systemctl set-default multi-user.target
vim /etc/default/grub
###
# remove
rhgb quiet
###
grup2-makeconfig -o /boot/grube2/grub.cfg

reboot
```    
7. Create a new 2GB volume group named "vgprac".

```bash
lsblk
fdisk 
n
+2G
w
pvcreate /dev/sdb1
vgcreate vgprac /dev/sdb1 

```

8. Create a 500MB logical volume named "lvprac" inside the "vgprac" yolume group.

```bash
lvcreate --name lvprac  --size 500M vgprac
``` 
9. The "lvprac" logical volume should be formatted with the xfs filesystem and mount
  persistently on the /mnt/lvprac directory.
```bash
mkfs.xfs /dev/vgprac/lvprac
mkdir /mnt/lvprac

``` 
10. Extend the xfs filesystem on "lvprac" by 500MB.
    
```bash
lvextend  --size +500M /dev/vgprac/lvprac /dev/nvme0n4p1


``` 
11. Use the appropriate utility to create a 5TIB thin provisioned volume.

```bash
vdo create --name vdoVolume --vdoLogicalSize 5T --device /dev/sdb2  
``` 

12.  Configure a basic web server that displays "Welcome to the web server" once
  connected to it. Ensure the firewall allows the http/https services.

```bash
yum install httpd -y
echo "Welcome to the Web Server " > /var/www/html/index.html

firewall-cmd --add-service=http --permanent
firewall-cmd --add-service=https --permanent

firewall-cmd --add-service=http
firewall-cmd --add-service=https 

firewall-cmd --list-all

systemctl restart httpd

``` 

13. Find all files that are larger than 5MB in the /etc directory and copy them to
  /find/largefiles
```bash
mkdir -p /find/largefiles
find /etc/ -size +5M -exec cp {} -rvfp /find/largefiles/ \; 
``` 
14. Write a script named awesome.sh in the root directory on system1.
- If "me" is given as an argument, then the script should output "Yes, I'm
   awesome."
- If "them" is given as an argument, then the script should output "Okay, they are
   awesome."
- If the argument is empty or anything else is given, the script should output
   "Usage ./awesome.sh me|them"

```bash
#!/bin/bash
if [ "$1" == "me" ] ; then
        echo "yes ,I'm awesome"
elif [ "$1" == "them" ]; then
        echo "Okay, they are awesome"
else
        echo " Usage ./awesome.sh me|them "
fi



``` 
15. Create users phil, laura, stewart, and kevin.
   - All new users should have a file named "Welcome" in their home folder after
   account creation.
   - All user passwords should expire after 60 days and be at least 8 characters in length.
   - phil and laura should be part of the "accounting" group. If the group doesn't
   already exist, create it.
   - stewart and kevin should be part of the "marketing" group. If the group doesn't
   already exist, create it.

```bash

touch /etc/skel/Welcome

vim /etc/login.defs 
####
PASS_MAX_DAYS   60
PASS_MIN_LEN    8

####

useradd phil 
useradd laura 
useradd stewart
useradd kevin
## check configuration
chage -l phile

groupadd accounting
usermod -aG accounting phil 
usermod -aG accounting laura 
groupadd marketing
usermod -aG marketing stewart  
usermod -aG marketing kevin 

```

16. Only members of the accounting group should have access to the "/accounting"
   directory. Make laura the owner of this directory. Make the accounting group the
   group owner of the "/accounting" directory.

```bash
mkdir /accounting
chgrp accounting /accounting/

chown laura /accounting/
chmod 770 /accounting/

``` 

17. Only members of the marketing group should have access to the "/marketing"
  directory. Make stewart the owner of this directory. Make the marketing group the
  group owner of the "/marketing" directory.
```bash
mkdir /marketing
chown stewart /marketing
chgrp marketing /marketing

```
18. New files should be owned by the group owner and only the file creator should
  have the permissions to delete their own files.
```bash
chmod  g+s  /marketing
chmod  +t  /marketing
chmod  g+s  /accounting
chmod  +t  /accounting
```
19. Create a cron job that writes "This practice exam was easy and I'm ready to ace my
   RHCSA" to /var/log/messages at 12pm only on weekdays.
```bash

systemctl status crond
systemctl enable --now crond

crontab -e 
#################
0 12 * * 1-5 logger "This practice exam was easy and I'm ready to ace my
   RHCSA"
#################

```

