# systemd

difference between systemd and init

init call services and wait for services to start and call other services
>call process in sequence

systemd call all services at same time
>call process in parallel


### init > to call services >  services have init script

### systemd > to call services >  services have unit file


systemd compatibles with init


init have multiple commands


systemd have systemctl

when systemd created they created journald

journald is a log 

bootloader > kernel > init > syslog
any service start before syslog doesn't have log


journal come to fix the problem
```
journalctl
```

evaluation of systemd

init    >  upstart  (ubuntu)   >   systemd(fedora) 

## HOL
get service status y
```
systemctl status <services>
systemctl status sshd
```
d on sshd for daemon


disable services  not start at boot
```
systemctl disable <services>
```
start services it will start once on session
```
systemctl start <services>
```
to stop services on current session
```
systemctl stop <services>
```
to enable services to start at boot
```
systemctl enable <service>
```


**********************************************
### on init 

to get status od services
```
service <service> status
```
to stop services
```
service <service> stop
```
to start services
```
service <service> start
```
disable services
```
chkconfig <service> off
```
enable services
```
chkconfig <service> on
```
**********************************************


to disable services even if u start it
the service will not start 
it will failed even if u start it
```
systemctl mask <service>
```

to enable service from mask
```
systemctl unmask <service>
```
**********************************************


# systemd targets or init runlevels = modes on windows 


init levels

0 = power off

1 = single user mode > give u root access to machine wihtout password

2 = multi user mode without NFS(network find system) ,GUI

3 = multi user mode without GUI . it called command line mode tty

4 = unused

5 = multi user mode with GUI

6 = reboot

>server most run on run level 3
systemd targets

multi-user.target = 3 

graphical.target = 5 runlevel

rescue.target  = 1st runlevel

reboot.target = 6

poweroff.target = 0


to get systemd default targets
it is  the target that is run on boot 
```
systemctl get-default
```
to set default target
```
systemctl set-default <target>
systemctl set-default multi-user.target

```
get runlevel
```
runlevel
```
convert from target to target on runtime

```
systemctl isolate <target>
systemctl isolate multi-user.target

```

on init to convert from runlevel to other
```
init <runlevelNumber>
```
the original files of systemd are in /user/lib/systemd

files on etc it shortcut for it
so when disable a service it remove the shortcut link


> systemd is dependancy system boot

unit file
```
[Unit]
Description=OpenSSH server daemon
Documentation=man:sshd(8) man:sshd_config(5)
After=network.target sshd-keygen.target
Wants=sshd-keygen.target

[Service]
Type=notify
EnvironmentFile=-/etc/crypto-policies/back-ends/opensshserver.config
EnvironmentFile=-/etc/sysconfig/sshd
ExecStart=/usr/sbin/sshd -D $OPTIONS $CRYPTO_POLICY
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=on-failure
RestartSec=42s

[Install]
WantedBy=multi-user.target
```


systemctl list units
it will list all units
```
systemctl list-units

```
list units files
```
systemctl list-unit-files
```

>systemctl restart <services>
>
>>it will stop and start services

>systemctl reload <services>
>
>>it will reload configuration while service running 



systemd |
        |
        - --/etc/systemd
        - --/user/lib/systemd   

if systemd don't  see configuration file on etc it will look on user/lib/systemd


