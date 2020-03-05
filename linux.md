# linux&shell

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
todo
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

---

##Selinux

```
/etc/sysconfig/selinux
```

