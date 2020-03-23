# /bin/bash 和/bin/sh的区别

### SH：

sh就是Bourne shell
 这个是UNIX标准的默认shell，对它评价是concise简洁 compact紧凑  fast高效，由AT&T编写，属于系统管理shell

### BASH:

bash是 GNU Bourne-Again SHell  (GNU 命令解释程序 “Bourne二世”)
 是linux标准的默认shell ，它基于Bourne shell，吸收了C shell和Korn shell的一些特性。bash是Bourne shell的超集，bash完全兼容Bourne shell,也就是说用Bourne shell的脚本不加修改可以在bash中执行，反过来却不行，bash的脚本在sh上运行容易报语法错误。

```
来源https://www.jianshu.com/p/070bd0b4855f
```

# 语法

在shell脚本中,变量赋值前后不要有空格

```shell
#e.g.
time1=$(date "+%Y%m%d%H%M%S")
```

## 获取命令行参数

test.sh

```shell
#!/bin/bash

echo $1
```

调用

```
~ ./test.sh  william
william
~ 
```

## &&   ||   ;

```
1. [ ; ] 
如果被分号(;)所分隔的命令会连续的执行下去，就算是错误的命令也会继续执行后面的命令。 
[root@localhost etc]# lld ; echo “ok” ; lok 
-bash: lld: command not found 
ok 
-bash: lok: command not found


2. [ && ] 
如果命令被 && 所分隔，那么命令也会一直执行下去，但是中间有错误的命令存在就不会执行后面的命令，没错就直行至完为止。 
[root@localhost etc]# echo “ok” && lld && echo “ok” 
ok 
-bash: lld: command not found


3. [ || ] 
如果每个命令被双竖线 || 所分隔，那么一遇到可以执行成功的命令就会停止执行后面的命令，而不管后面的命令是否正确与否。如果执行到错误的命令就是继续执行后一个命令，一直执行到遇到正确的命令为止。 
[root@localhost etc]# echo “ok” || echo “haha” 
ok 
[root@localhost etc]# lld || echo “ok” || echo “haha” 
-bash: lld: command not found 
ok
```

## \$PWD

和 $(pwd)等效，环境变量，表示当前工作路径

和pwd是不同的，pwd是命令



# 如何自定义一个命令

写一个可执行文件(demo如下)

```shell
#!/bin/bash

echo $@
```

放到PATH下即可



# 在某个平台编译

##1.从源码进行编译

可以编译为二进制文件（可执行文件）



## 2.可以从src.rpm包进行编译

keepalived-1.3.5-1.el7.src.rpm 

可以编译为rpm包

也可以直接编译为可执行文件



Linux下二进制包、源代码包、rpm包](https://www.cnblogs.com/cj2014/p/3728324.html)

主要提供三种格式的mysql包：rpm格式、二进制格式、源码格式：（tar打包，gz压缩）

rpm格式： libjpeg-devel-6b-33.x86_64.rpm    #rpm格式很好区分，

二进制包： mysql-3.23.58-pc-linux-i686.tar.gz  #二进制格式的包名字很长，有版本号、适应平台、适应的硬件类型等，格式：mysql-<版本>-<OS>-tar.gz

源码包：   php-5.2.14.tar.gz               #而源码格式仅仅就是一个版本号的tar包。#cj 安装区别：解压、./config、make、make install

 

source code 是程序员写的码， 
binary code 是机器跑的码。 
source code 得经过 compile 才能成为 binary code 。 

RPM 有分兩種：binary rpm 跟 source rpm 。 
前者是編好的 binary ，安裝就可用。 
後者是還沒編好的 source ，需 rebuild 之後才能安裝

 

源代码方式和二进制包是软件包的两种形式。二进制包里面包括了已经经过编译，可以马上运行的程序。你只需要下载和解包（安装）它们以后，就马上可以使用。源代码包里面包括了程序原始的程序代码，需要在你的计算机上进行编译以后才可以产生可以运行程序,所以从源代码安装的时间会比较长。

 

源码的安装一般由3个步骤组成：**配置(configure)、编译(make)、安装(make install)**。