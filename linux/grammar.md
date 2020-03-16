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