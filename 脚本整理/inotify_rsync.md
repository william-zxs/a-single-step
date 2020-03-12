#利用inotify+rsync实现远程目录实时增量备份

## client：负责监控目录并推送数据

client.sh 

运行  nohup ./client.sh > client.log 2>&1 &

```shell
#!/bin/bash
#chkconfig: 2345 80 90
#description: inotify autostart service.

# sync folder to be synced in this server
src_tobe_synced=/var/jhrsync

# 同步接收方ip
remote_nginx_ip=192.168.1.20

# sync receiver's rsync module name
dest_module_name=demo_backup_module

# sync receiver's authentication username
remote_auth_user=admin_backuper

set -x

/usr/bin/inotifywait -mrq --timefmt '%Y/%m/%d-%H:%M:%S' --format '%T %w %f' -e modify,delete,create,move,attrib $src_tobe_synced | while read file
do
# 默认rsync daemon端口是873，也可以指定端口 --port 
/usr/bin/rsync -vzrtopgl --port=8085 --progress --delete --password-file=/etc/rsyncd.passwd $src_tobe_synced $remote_auth_user@$remote_nginx_ip::$dest_module_name

echo "${file} was rsynced" >> /var/log/jhrsync.log 2>&1

done

set +x

```

rsyncd.passwd 

  (位置在client.sh中指定，一般放于/etc/rsyncd.passwd,  注意权限**：chmod 600 /etc/rsyncd.passwd** )

```
1234abcd
```





##server:接收数据

第一步：编辑rsync配置

/etc/rsyncd.conf

```conf
pid file = /var/run/rsyncd.pid
port = 873
address = 192.168.1.20
uid = root
gid = root

use chroot = yes
read only = no

hosts allow=192.168.1.15
hosts deny=*

max connections = 5
motd file=/etc/rsyncd.motd
lock file=/var/run/rsyncd.lock
log file =/var/log/rsyncd.log

log format = %t %a %m %f %b
syslog facility = local3
timeout = 300


[demo_backup_module]   ## 自定义模块名，及对应用户和文件保存目录
path = /var/jhrsync
list=no
ignore errors
comment = demo config backup
auth users = admin_backuper
secrets file = /etc/rsyncd.secrets
```

第二步：编辑 rsyncd.secrets 

/etc/rsyncd.secrets 

```
admin_backuper:1234abcd
```

chmod 600 rsyncd.secrets

第三步：启动脚本

start_rsync_server.sh

```shell
#!/bin/bash
rm -rf /var/run/rsyncd.pid
/usr/bin/rsync --daemon --config=/etc/rsyncd.conf
```

