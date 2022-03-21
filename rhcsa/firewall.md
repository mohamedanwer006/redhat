# FireWall

### list all services
```
firewall-cmd --list-all
```
### open port
```
firewall-cmd --permanent --add-port=<port>/tcp
firewall-cmd --reload
```
### close port
```
firewall-cmd --permanent --remove-port=<port>/tcp
firewall-cmd --reload
```
### open port for specific service
```
firewall-cmd --permanent --add-service=<service>
firewall-cmd --reload
```
### close port for specific service
```
firewall-cmd --permanent --remove-service=<service>
firewall-cmd --reload
```




