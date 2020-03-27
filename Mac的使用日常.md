#homebrew

##查看brew install 安装的路径

```
#~ brew list mongo
/usr/local/Cellar/mongodb/4.0.3_1/.bottle/etc/mongod.conf
/usr/local/Cellar/mongodb/4.0.3_1/bin/mongo
/usr/local/Cellar/mongodb/4.0.3_1/bin/mongod
/usr/local/Cellar/mongodb/4.0.3_1/homebrew.mxcl.mongodb.plist
```

#launchctl

launchctl 通过.plist 文件管理Mac os中的进程

 .plist文件中定义了程序的启动命令



- LaunchDaemons `~/Library/LaunchDaemons`
  用户登陆前运行 plist（程序）
- LaunchAgents `~/Library/LaunchAgents`
  用户登录后运行相应的 plist（程序）



显示.plist文件

```
launchctl list
```

```
#~ launchctl list | grep mongo 
38618	0	homebrew.mxcl.mongodb
```



自定义启动/关闭命令

* A :

  ```
  1. vim ~/.bash_profile #编辑添加如下脚本 
  2. 命名别名（以 nginx 为例）
      >启动：alias nginx.start=’launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist’ 
      >关闭：alias nginx.stop=’launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist’ 
      >重启：alias nginx.restart=’nginx.stop && nginx.start’ 
  ```

  

* B:

  名称是 launctl list 中的名称

  ```
  alias mongodb.start='launchctl start homebrew.mxcl.mongodb' 
  alias mongodb.stop='launchctl stop homebrew.mxcl.mongodb'
  ```

  



