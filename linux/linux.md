#时间

linux中的时间分为系统时间和硬件时间



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



# Console 

**Console 和 Terminal**



ctrl+alt+f1 ..... f6

 ctrl+alt+f7 图形界面

 # linux文件的尾缀
 .png 和 .jpeg 可以随便改，因为linux文件的尾缀只是一个标示的作用。

 # su
 ```
 su - username  可以使用username 的环境变量
 ```