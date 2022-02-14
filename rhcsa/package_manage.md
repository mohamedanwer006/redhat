# package manager

code -> compile -> run

python /custom library  

there is problem in distribution

solution:

source code -> compile -> binary + assets + other files

all of this is in one packages

like exe ,msi on windows
- redhat -> rpm
- debian -> deb
- apple -> dmg


## dependancy 
### dependancy resolution
install package1 depend on package2 and so on


with source code install u have problems
 - compile -> binary
   - bin/sbin
 - fonts
 - remove 


## yum 
server yum server 
- packages
- metadata for packages dependencies

yum client
- install package

yum used rpm as backend

yum use metadata to resolve dependancy

it's not override the rpm

## yum basic installation
### search for package

```bash
yum search <packageName>
yum search vim
```
download metadata only . xml files
download database metadataFiles for packages 

you  download metadata only if connect for first time or server update metadata


### yum server or repo server ||
local or connected to internet

all you need as client is address for server

list  configured yum server
```bash
yum repolist

```
it's under /etc/yum.repos.d/centos

remove any apps
```
yum remove <package>
yum remove vim
```
yum will remove only the package  not dependancy

## get info about package
```
yum info <packageName>
```

you need to install apache ssl python ....


```bash
yum grouplist
```
```bash
yum groupinstall <groupName>

yum groupinstall "Basic Web server "
# install GUI
yum groupinstall "Server With GUI"
``` 

## yum update

```bash
# update all package
yum update  
# update specific package
yum update <packageName>
```

To know the package install specific file 
```bash

yum provides <file>
yum provides /etc/sysctl.conf
```
> anaconda installer of redhat


```bash
yum clean <option>
#OR
#clean all 
yum clean all

```

to cache packages
```bash
#let keep_cache= 1 
# /etc/yum.conf

# it will cache package on /var/cache/yum 
```

get yum history
```bash
yum history
# for one transaction information
yum history info <transactionNumber>

#undo of transaction
yum history undo <transactionNumber>

```

install & remove rpm package
```bash
#install
rpm --install <package>
rpm --install httpd-2.6-45.el7.x86_64.rpm
rpm -i httpd-2.6-45.el7.x86_64.rpm
rpm -ivh httpd-2.6-45.el7.x86_64.rpm

#v=verbose
#h=hashed ##%

# remove
rpm --erase httpd
rpm -e httpd

```
## query all package install on the system
```bash
rpm -qa
# get information not installed
rpm -qpi <packageName.rpm> 
# already install
rpm -api <packageName> 
# upgrade or install if it's not install
rpm -Uvh <newPackage>

#Freshen . this will upgrade but only one is installed before
rpm -Fvh <newPackage>
#query configuration file
rpm -qc <packageN  ame>

#use p if the package not installed
```
## How to trust package
```bash
Any package from redhat have sign (key)

rpm -K <package>

#keys found in /etc/pki/rpm-gpg/

rpm --import <key>   
# remove key
rpm -e <key>


```

this rpm method  will fail if there is dependancy not installed

```bash
yum localinstall <full-package-name>   
# it will install missing dependancy if needed
```








## YUM server machine


to make yum server you need web server ftp or http to share package

 - install vsftpd 
 - start services

need package and 
metadata -> install createrepo will help create xml metadata

```
createrepo -v /var/ftp/pub/Package/
```
ftp host file from  /var/ftp/pub

allow ftp port on firewall
```
firewall-cmd --add-service=ftp --permanent
```

## YUM client machine
 -  install ftp
 
configuer server on /etc/yum.repos.d/

`vim Local-Server.repo`
```
[Local-Server]
name=Local Yum Server
baseurl=ftp://192.168.100.129/pub/Packages
enabled=1
gpgcheck=0 
#if gpg key enable
#gpgcheck=1
#gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
```










