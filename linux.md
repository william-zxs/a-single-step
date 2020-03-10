# linux

##expect

用于脚本登陆服务器并执行命令。

```shell
#!/usr/bin/expect -f

set timeout 10
spawn ssh -p 36408 root@114.242.206.180

expect "]#" {send "mysql  -uroot -pabc123 -e 'create database  IF NOT EXISTS $env(DBNAME)  charset=utf8;'\r"}
expect "]#" {send "mysql -uroot -pabc123  $env(DBNAME) < ~/data/community.sql\r" }
expect "]#" {send "mongorestore -d $env(DBNAME) ~/data/community\r" }
send "exit\r"
expect eof
```

---

##EOF

```

[worker@iZ8vb1umb9zfnw5rvg4577Z data_to_docker]$ cat restore_to_docker.sh 
#!/bin/sh

db=community
pass=abcd1234
host=172.26.99.100
sqlport=8306
mongoport=47017

mysqladmin -u root -p"${pass}" -h $host -P $sqlport drop $db
mysql -u root -p"${pass}" -h $host -P $sqlport < $1

mongo  $host:$mongoport <<EOF
use $db;
db.dropDatabase();
exit;
EOF

mongorestore -h $host:$mongoport -d $db $2
```

---

##SSH

###ssh-copy-id user@host

将本机公钥传到服务器

-i 选项可以指定公钥文件

###.ssh config

**配置快速登陆以及代理登陆**

```shell

Host name1
    HostName 19.38.112.123
    Port 22
    User worker

Host name2
    HostName 124.222.226.220
    Port 36408
    User crs 
    ProxyCommand ssh user@name1 -W %h:%p
    

ssh name2
```

---

##rsync

**rsync 指定端口推送**

```
rsync -av -e 'ssh -p 36408' $bdir crs@114.242.206.180:~/aliyun/
```

**rsync指定代理推送**

```
rsync -vrtopz --progress -e ' ssh -ax -c blowfish ' xx@ip1:/data/  /data1/
```

---

##tar

```
todo
```

---

##nohup  2>1&

```
todo
```

---

##systemctl

```
查看防火墙状态
systemctl status firewalld

设置开机自动启动（本质上是创建了链接）
systemctl enable mariadb
Created symlink from /etc/systemd/system/multi-user.target.wants/mariadb.service to /usr/lib/systemd/system/mariadb.service.



查看开机项
syatemctl list-unit-files |grep  mysql
```

**利用systemctl命令管理**

```
利用systemctl命令管理
显示服务状态：systemctl status docker.service
列出服务层级和依赖关系：systemctl list-dependencies docker.service

启动服务：systemctl start docker.service
关闭服务：systemctl stop docker.service
重启服务：systemctl restart docker.service

设置服务自启动：systemctl enable docker.service
禁止服务自启动：systemctl disable docker.service

查看服务是否自启动：systemctl is-enabled docker.service
列出系统所有服务的启动情况：systemctl list-units --type=service
列出所有自启动服务：systemctl list-unit-files|grep enabled


```

**对应的旧指令（chkconfig、service）**

```
对应的旧指令（chkconfig、service）
显示服务状态：service docker status
列出服务层级和依赖关系：systemctl list-dependencies docker.service

启动服务：service docker start
关闭服务：service docker stop
重启服务：service docker restart

设置服务自启动：chkconfig --level 3 docker on
禁止服务自启动：chkconfig --level 3 docker off

查看服务是否自启动：chkconfig --list docker
列出系统所有服务的启动情况：chkconfig --list
```







---

##Selinux

```
/etc/sysconfig/selinux
```



##备份(及恢复)mysql、mongo

###备份

```
#/bin/sh

mysqldump -p'lott-jh-abcd1234' --data community > community_`date +%m%d%H%M`.sql
mongodump  -d community -o mongo_community_`date +%m%d%H%M`
```

### 恢复

```
#!/bin/sh

db=community
pass=abcd1234
host=172.26.99.100
sqlport=8306
mongoport=47017

mysqladmin -u root -p"${pass}" -h $host -P $sqlport drop $db
mysql -u root -p"${pass}" -h $host -P $sqlport < $1

mongo  $host:$mongoport <<EOF
use $db;
db.dropDatabase();
exit;
EOF

mongorestore -h $host:$mongoport -d $db $2
```



## ARP

```
todo
linux 中的ip  mac 映射
```

## crontab

定时任务

## awk &  xargs

ps -ef | grep zabbix_server | awk '{print $2}' | xargs kill -9 



## netstat

```
-a : 显示所有socket
-t : 指明显示TCP端口
-u : 指明显示UDP端口
-l : 仅显示监听套接字(所谓套接字就是使应用程序能够读写与收发通讯协议(protocol)与资料的程序)
-p : 显示进程标识符和程序名称，每一个套接字/端口都属于一个程序。
-n : 不进行DNS轮询，显示IP(可以加速操作)

查看程序/进程 的端口使用情况
netstat -nlp | grep rsync
netstat -nlp | grep 22010(pid)

查看端口使用情况
netstat -an | grep 3306 (port)
```

##用户和用户组

Linux下的用户属于与它同名的用户组，这个用户组在创建用户时同时创建

```
useradd -d /home/jack -m jack

userdel -r jack

passwd jack
```
