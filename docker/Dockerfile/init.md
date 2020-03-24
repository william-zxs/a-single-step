



```shell
#!/bin/sh

if [ -x $1 ];then
   exec  $@  
   exit 0
fi

exec  /usr/bin/redis-server $@
```

前面的if  -x 条件是 第一个参数是否可执行。

