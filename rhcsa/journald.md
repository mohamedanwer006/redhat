# Journald service

Print logs 
```
journalctl
```
Print logs no page
```
journalctl --no-pager
```

Print logs in reverse
```
journalctl -r
```
Print logs like tail -f
```
journalctl -f
```
Print logs for specific date
```bash
journalctl --since <date>
journalctl --since "22021-10-8"
journalctl --since yesterday
journalctl --since today
# since  start date : until stop date
journalctl --since "2021-10-8" --until "2021-10-9"
```

Print last boot Ids
```
journalctl --list-boot
```
Print from boot id
```bash
journal -b <bootID>
```
Filter logs for specific services

```bash
journalctl -u sshd
journalctl -u crond
```
Filter logs for kernel

```bash
journalctl -k
```


## Persistent Journal Logs 
1. create the directory (/var/log/journal)
```
mkdir /var/log/journal
```
2. restart the systemd-journald service
```
systemctl restart systemd-journald
```

3. verify the journal directory
```
ls -l /var/log/journal
```


