# mysql

## mysql 引擎

默认是 InnoDB

---

## 注意点

隔离级别



##mysqladmin

```
修改密码（初始化密码）
mysqladmin -u root -p[oldpassword] password abc123

创建数据库，删除数据库

```



## mysqldump

```shell
#在备份时候注意binlog的备份
mysqldump -h 192.168.1.100 -P 3306 -uroot -pabc123 --flush-logs  --single-transaction --data community > $bdir/community.sql
```









##LOCK

UNLOCK TABLES还还以用来释放FLUSH TABLES WITH READ LOCKS

## 同步

异步复制   全同步复制   半同步复制

## 锁

乐观锁和悲观锁



## 遇到的问题

### 数据库连接错误

```
show global variables like ‘wait_timeout’;
| Variable_name | Value |
+---------------+-------+
| wait_timeout  | 28800 |


Flask-SQLALchemy
SQLALCHEMY_POOL_RECYCLE

mysql的默认超时时间是8小时
Flask-SQLALchemy的默认超时时间是2小时




```

## mysql常用查询

