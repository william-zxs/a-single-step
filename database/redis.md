# 持久化存储



redis_netlock

使用redis做锁，



交集，并集，差集。







##阿里二面：熟悉Redis？讲讲你理解的Redis的持久化机制(RDB、AOF


# redis 事务
redis事务是redis的最小执行单元
```
multi
INCR user_id
INCR user_id
exec
```

# watch
WATCH命令可以监控一个或多个键，一旦其中有一个键被修改（或删除），之后的事务就不会执行。监控一直持续到EXEC命令（事务中的命令是在EXEC之后才执行的，所以在MULTI命令后可以修改WATCH监控的键值）
