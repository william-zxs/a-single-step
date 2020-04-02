#exec  source  sh

source 和 . 不启用新的shell，在当前shell中执行，设定的局部变量在执行完命令后仍然有效。

bash 或 sh 或 shell script 执行时，另起一个子shell，其继承父shell的环境变量，其子shelll的变量执行完后不影响父shell。

exec是用被执行的命令行替换掉当前的shell进程，且exec命令后的其他命令将不再执行。

shell 的内件命令exec执行命令时，不启用新的shell进程。





# set -e

```
#!/bin/bash

set -e

command 1
command 2
...

exit 0
```

这句语句告诉bash如果任何语句的执行结果不是true则应该退出