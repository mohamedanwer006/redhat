# network manager

### show ip address
```
ip address show
ip a s
```
```
ifconfig
```
### loopback interface (lo)
        127.0.0.1       localhost
        ::1             localhost

    it's virtual interface .
    make sure that tcp/ip stack implementation is working

### disable interface
```
ifdown <interface>
```
###  enable interface
```
ifup <interface>
```

### Gateway vs default gateway
Gateway is rote to specific network
Default Gateway is rote to all network (internet)


## In network administration
>layer 2 default gateway   can't Transmit between different network
>layer 3 default route can transmit from network to network


## network manager
network manager is a tool to manage network

### **Profiles**

### configure profile
```bash
 # show all profile
nmcli connection show 
 # show specific profile
nmcli connection show <profileName>


nmcli con add con-name <profileName> ifname <interfaceName> type ethernet ipv4 <ipAddress> gw4 <gateway>   

```



