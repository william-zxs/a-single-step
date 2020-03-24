# linux

Linux系统是一个多用户多任务的分时操作系统

Linux内核作为一个通用操作系统，需要兼顾各种各样类型的进程，包括实时进程、交互式进程、批处理进程等。不同的进程采用不同的调度策略，目前Linux内核中默认实现了4种调度策略，分别是deadline、realtime、CFS和idle，它们分别使用struct sched_class来定义调度类



# /etc

##/etc/passwd

/etc/shadow  和 /etc/passwd每一行一一对应，

/etc/shadow 保存了密码等等信息。

###批量添加用户

```
newusers < user.txt
chpasswd <pass.txt
pwunconv
/usr/sbin/pwconv
等等命令
```





## /etc/group

保存了分组信息

将用户分组是Linux 系统中对用户进行管理及控制访问权限的一种手段。

每个用户都属于某个用户组；一个组中可以有多个用户，一个用户也可以属于不同的组。



## /etc/bashrc

/etc/profile:此文件为系统的每个用户设置环境信息,当用户第一次登录时,该文件被执行，并从/etc/profile.d目录的配置文件中搜集shell的设置，
/etc/bashrc:为每一个运行bash shell的用户执行此文件，当bash shell被打开时,该文件被读取。
~/.bash_profile:每个用户都可使用该文件输入专用于自己使用的shell信息,当[用户登录](https://www.baidu.com/s?wd=用户登录&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)时,该文件仅仅执行一次!默认情况下,他设置一些环境变量,执行用户的.bashrc文件。
~/.bashrc:该文件包含专用于你的bash shell的bash信息,当登录时以及每次打开新的shell时,该文件被读取。



~/.bashrc:该文件包含专用于某个用户的bash shell的bash信息,当该用户登录时以及每次打开新的shell时,该文件被读取.

~/.bash_profile: 每个用户都可使用该文件输入专用于自己使用的shell信息，当用户登录时，该文件仅仅执行一次!默认情况下,他设置一些环境变量,执行用户的.bashrc文件。
~/.bash_logout: 当每次退出系统(退出bash shell)时，执行该文件。
~/.bash_profile 是交互式、login方式进入bash运行的，~/.bashrc是交互式non-login方式进入bash运行的，通常二者设置大致相同，所以通常前者会调用后者。