#homebrew

##查看brew install 安装的路径

```
#~ brew list mongo
/usr/local/Cellar/mongodb/4.0.3_1/.bottle/etc/mongod.conf
/usr/local/Cellar/mongodb/4.0.3_1/bin/mongo
/usr/local/Cellar/mongodb/4.0.3_1/bin/mongod
/usr/local/Cellar/mongodb/4.0.3_1/homebrew.mxcl.mongodb.plist
```

# launchctl

launchctl 通过.plist 文件管理Mac os中的进程,brew 安装的程序都会生成一个.plist

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

  



#Chrome

当连接http 请求时，chrome 提示不安全，没有高级   继续的按钮，

在chrome该页面上，直接键盘敲入这11个字符：`thisisunsafe`


# Terminal
## 科学上网
```
brew install privoxy

listen-address 0.0.0.0:8118
forward-socks5 / localhost:1080 .


sudo /usr/local/sbin/privoxy /usr/local/etc/privoxy/config

netstat -na | grep 8118

export http_proxy='http://localhost:8118'
export https_proxy='http://localhost:8118'

unset http_proxy
unset https_proxy


vim ~/.bash_profile
-----------------------------------------------------
export http_proxy='http://localhost:8118'
export https_proxy='http://localhost:8118'
-----------------------------------------------------


function proxy_off(){
    unset http_proxy
    unset https_proxy
    echo -e "已关闭代理"
}
function proxy_on() {
    export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"
    export http_proxy="http://127.0.0.1:8118"
    export https_proxy=$http_proxy
    echo -e "已开启代理"
}
```

打开当前文件夹
```
open .
```