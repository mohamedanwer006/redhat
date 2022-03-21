# NTP configuration

### Helps keep accurate time keeping
## Configure time sync using crony

# Chrony

It works as ntp client and ntp server.

installation setup:

### NTP server: 192.168.56.102
### NTP client: 192.168.56.101

## On Server: 

```bash
# ping <server>  from client
ping 192.168.56.102
# ping <client>  from server
# if not install

yum install chrony 

# start chrony at boot
systemctl start chronyd
systemctl enable chronyd
# or
systemctl enable --now chronyd 

# check chrony status
systemctl status chronyd

# configure chrony
vi /etc/chrony.conf
# allow NTP client to access the server
# uncomment the following line
# allow <ipv4 address of local network >
systemctrl restart chronyd

# allow inbound access to the server
firewall-cmd --permanent --add-service=ntp
firewall-cmd --reload


```

## On Client 

```bash
# ping <server>  from client
ping 192.168.56.102
# ping <client>  from server
# if not install
yum install chrony 

# start chrony at boot
systemctl start chronyd
systemctl enable chronyd
# or
systemctl enable --now chronyd 

# check chrony status
systemctl status chronyd

timedatectl set-ntp true
# check active
timedatectl

# configure chrony as client
vi /etc/chrony.conf

# goto to server pool and comment out the following line
# pool <server> iburst
# add server ip
server <server ip>

#restart chrony
systemctl restart chronyd

# check  
chronyc sources

```

### On server get connected clients:
````
chronyc clients
```