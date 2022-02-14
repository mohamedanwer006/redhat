
# boot
1. before os load
2. after os load

## before os load
BIOS (Basic Input/Output System)
1. POST (power on self test)
    - test hardware
2. find bootable devices and compare with its setting (DVD ,HDD ...etc)
3. load IPL (Initial Program Loader) small program to call bootable devices (bootloader) called Grub (GNU GRand Unified Bootloader)
4. load /start bootloader Grub (Grand Unified Bootloader)
5. Bootloader =>load kernel
6. kernel => load init process or systemd on rh7 and above
7. systemd /init call services /daemons

> hint 
## MBR (Master Boot Record)
 - partition table 64byte
 - bootloader 446byte
 - magic number 2byte
---
## bootloader
### divided into two parts
1. first stage => MBR
    - its purpose to call second stage
2. second stage => DISK /boot 
    - call kernel

## kernel
### divided into two parts
1. kernel
    -core of kernel  (vmlinuz)
    > memory footprint use less memory 
        >> load time  fast
2. initramfs on rh7 >/ initrd  in <rh6
    - drivers and modules

> when kernel load mount root filesystem read only if there is no fail it remount root filesystem read write


 