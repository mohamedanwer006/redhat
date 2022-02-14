# bootloader

MBR 
1. partition table 64byte
2. bootloader 446byte
    - first stage
3. magic number 2byte

all bootloader file in /boot/
- kernel vmlinuz & initramfs / initrd
- bootloader grub
  
> grub = GRand Unified Bootloader 
grub2 support boot multiple os , password for bootloader

 
on /boot
- grub2
config file of grub2 on /boot/grub2/grub.cfg

soft link on /etc/grub2.cfg => role that all config file on etc


# kernel 
    - kernel 
    - initramfs (initrd) 

`kernel name vmlinuz`

but driver on initramfs 
> have module and driver
if there fail on driver the kernel still untouched

when kernel load mount root filesystem read only if there is no fail it remount root filesystem read write

after kernel load 

it will call init process or systemd on rh7 and above



bootloader > kernel > systemd > services / daemons 



