# Run container as service

```bash
vim  /etc/systemd/system/<container-name>.service

#### add the following lines

[Unit]
Description=container service demo
Wants=syslog.service

[Service]
Restart=always
ExecStart=/usr/bin/podman start -a <container-name>
ExecStop=/usr/bin/podman stop -t 5 <container-name>


[Install]
WantedBy=multi-user.target


####


```

```bash
systemctl deamon-reload
systemctl enable <container-name>.service
systemctl start <container-name>.service
systemctl status <container-name>.service
```


## mount local directory to container
```bash
podman run -it --privileged --name <container-name> -v /home/<user>/<local-dir>:/<container-dir> <image-name>
# example : mount /home/app to /app in container
podman run --privileged -it --name httpd-server -v /home/app:/app httpd /bin/bash
```

