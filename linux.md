# linux&shell



### expect

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

### EOF

```
todo
```

