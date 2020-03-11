#linux

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

##nohup   

nohup  [command]  >file 2>&1  &

```
nohup 是不挂断，即当前shell关闭之后，程序不会接受挂断的信号
>file 将标准输出输出到file
2>&1 将错误输出重定向到标准输出 
& 放在命令末尾，表示后台运行，防止终端被某个进程占用，终端关闭，进程也会停止。
```

```
> file 将标准输出输出到file，相当于 1>file
2> errorfile  将错误输出到errorfile
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
关闭服务：systemctl stop docker.serviced
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



## rpm

安装一个包

```
rpm -ivh
```

升级一个包

```
rpm -Uvh
```

卸载一个包

```
rpm -e
```

查询一个包是否被安装

```
rpm -q  <name>
rpm -qa | grep <name>  (列出所有被安装的rpm包)
```

得到被安装的包的信息

```
rpm -qi <name>
```

列出服务器上的一个库属于哪个rpm包

```
rpm -qf
```

```
.src.rpm
这类软件包是包含了源代码的rpm包，在安装时需要进行编译
rpm2cpio  demo.src.rpm  | cpio -id   可以得到demo的源码
```



## yum

```
yum install
```

列出所有可安装的软件

```
yum list
```

删除包

```
yum remove
```

查找软件包

```
当我们想用一些命令但是又想不起来这个命令属于哪个包时 可以使用这个命令 比如 查找killall属于哪个包
yum search killall
yum install +找到的包名
```

列出当前yum源

```
yum repolist
```

对于 Linux 软件安装时提示缺失库的，可以使用 yum 的 provides 参数查看 libstdc++.so.6 的库文件包含在那个安装包中只需要执行：

```
yum provides libstdc++.so.6
```

下载rpm包

```
yumdownloader keepalived

下载.src.rpm源码包
yumdownloader --source keepalived
```



### 搭建自己的yum源

createrepo

### 挂载镜像作yum源

1.mount 挂载镜像到指定目录

2.repo 中baseurl指向该目录（e.g.   baseurl=file:///media/   ）

## demsg

 demsg命令用于显示开机信息，内核会将开机信息存储在系统缓冲区（ring buffer）中，开机后可用dmesg命令查看，也可以在/var/log/目录中查看dmesg文件

## journalctl

日志管理工具journalctl是centos7上专有的日志管理工具，该工具是从message这个文件里读取信息。

## gcc、Make、CMake

gcc 是GNU编译器套件，是Linux下默认的C/C++编译器.

CMake 是一个跨平台的编译工具。事实上Cmake并不直接构建出最终的软件，而是产生不同平台标准的构建档(如 Unix的Makefile 或是 Windows Visual C++的 projects/workspaces),然后再依一般的构建方式使用。 

Make 通过编写的`makefile`脚本文件描述整个工程的编译、链接规则；通过脚本文件，对于复杂的工程也可以只通过一个命令就完成整个编译过程



## kill

killall

killall可以根据名字来杀死进程

```
killall nginx
killall -9 nginx
```

killall [参数] name

参数：-r正则



kill

列出所有信号

```
kill -l 
```

彻底杀死

```
kill -9  2324
```





 



# TODO

## mount

###如何写一个systemctl管理的service



