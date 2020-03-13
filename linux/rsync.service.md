#实现一个systemctl管理的service

rsync.service

```shell
[Unit]

Description=The jhrsync server



[Service]

Type=simple

PIDFile=/var/run/jhrsync.pid

ExecStartPre=/usr/bin/rm -f /var/run/jhrsync.pid

ExecStart=/usr/local/jhrsync/jhrsync.sh

ExecReload=/bin/kill -s HUP $MAINPID



[Install]

WantedBy=multi-user.target
```



将rsync.service 加入到

```
/usr/lib/systemd/system
```

目录中

即可用systemctl 命令进行管理

```
systemctl status rsync
systemctl start rsync
systemctl stop rsync

加入开机自启动
systemctl enable rsync
关闭开机自启动
systemctl disable rsync 
```

