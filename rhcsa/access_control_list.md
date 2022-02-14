# access control list
Full control of giving access to user for specific resources

To get file access control list (ACL)
```bash
# getfacl <path>
getfacl /etc/passwd
```
give access to user
```bash
# setfacl <acl> <path>
# setfacl -m u:<user>:<permission> <path>
# -m fo append to existing permissions
setfacl -m u:root:rw /etc/passwd

# set acl for directory and sub files
setfacl -R -m u:root:rw /etc/
# set default acl for directory and sub files
setfacl -m d:u::rwx /etc/

```
