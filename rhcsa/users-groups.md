root user id : 0
services user id , 1 : 999
user id >=1000
> by default when create user a group created with that name it's the primary group  its called user primary group it's user private group

> user can have mutiple secondry group

create user
```
useradd <userName>
useradd -c <comment> -d <directory> -g <group> -G <group> -m <userName>
```
remove user
```
userdel <userName>
```
change user password
```
passwd <userName>
```
create group
```
groupadd <groupName>
```
remove group
```
groupdel <groupName>
```
change group password
```
passwd <groupName>
```
add user to group
```
usermod -a -G <groupName> <userName>
```
remove user from group
```
usermod -r -G <groupName> <userName>
```
# permissions
fileType userPermission groupPermission otherPermission

fileType: i bit = d , l , c , b , -

d = directory
l = symbolic link
c = character device
b = block device
**-** = file 


userPermission: 3 bit = r , w , x , -

groupPermission: 3 bit  = r , w , x , - 

otherPermission: 3 bit = r , w , x , -

## For example:
```
drwxr-xr-x
```
d = directory

userPermission (u): rwx = read, write, execute

groupPermission (g): r-x = read, execute

otherPermission (o): r-x = read, execute

change user permission
```
chmod <permission> <fileName>
```
for example:

use +to add permission

`chmod g+wx <fileName>` 

`chmod u+x <fileName> ` 

`chmod g-r <file name>` use - to remove permission

```
chmod 755 <fileName>
```
7 = 111 => rwx

6 = 110 => rw-

5 = 101 => r-x

>4 = 100 => r--

3 = 011 => -wx

>2 = 010 => -w-

>1 = 001 => --x

0 = 000 => ---

change permission for directory and its files
```
chmod -R <permission> <directoryName>
```

change user owner
```
chown <userName> <fileName>
```
change group owner
```
chown :<groupName> <fileName>
```
change user and group owner
```
chown <userName>:<groupName> <fileName>
```
