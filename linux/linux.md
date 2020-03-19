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

