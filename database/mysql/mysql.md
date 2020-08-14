# mysql

## mysql 引擎

默认是 InnoDB

---

## 注意点

隔离级别



##mysqladmin

```
初始化密码
mysqladmin -u root  password abc123
修改密码
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



#pymysql

注意字符集要用utf8mb4

```python
DB_URI = 'mysql+pymysql://{}:{}@{}:{}/{}?charset=utf8mb4'.format(USERNAME, PASSWORD, HOSTNAME, PORT, DATABASE)
```

## 字符集问题   存储emoji

UTF-8编码有可能是两个、三个、四个字节。Emoji表情是4个字节，而Mysql的utf8编码最多3个字节，所以数据插不进去。

mysql的utf8并不是真正意义上的utf8，mysql的utf8只支持最长三个字节,所以Emoji 表情和有些生僻字以及任何新增的 Unicode 字符等如果超过三个字节用utf8字符集保存是会报错的。mysql在5.5.3之后增加了utf8mb4这个字符集，mb4就是most bytes 4的意思，专门用来兼容四字节的unicode。好在utf8mb4是utf8的超集，除了将编码改为utf8mb4外不需要做其他转换。

       为了获取更好的兼容性，应该总是使用 utf8mb4 而非 utf8.  对于 CHAR 类型数据，utf8mb4 会多消耗一些空间，根据 Mysql 官方建议，使用 VARCHAR  替代 CHAR。
    
       因为mysql的char列类型在utf8mb4下, 为了保证所有的数据都存的下, char将会占用字符数*4的字节数 (mysql的char列类型utf8将占用字符数*3的字节数), 以保证空间分配足够. 所以建议用可变长度varchar, 以节省空间. 可变长度消耗的存储空间为: 实际存储需要的字节数+1或2个字节表达的长度





# like

```
select * from user where name like "Will%";

select * from user where name like "%张先森";

select * from user where name like "%ill%";
```

第一种和第二种会触发索引，第三种不会。



# 关键字

mysql不能用order作为表名，因为order是mysql 的关键字，用order作为表名会出现问题。





#mysql复制策略：

异步复制  

半同步复制 （至少保证一个从库同步了binlog）

全同步复制





# 外间约束

  **SET FOREIGN_KEY_CHECKS=0;**





#varchar

假设  类型为varchar(100)   的字段存了 字符串 “abc”。

实际占用的存储是三个字符，但是读取的时候，会分配100字符的内存。





#float double decimal

浮点数：float单精度        double双精度

定点数：decimal  金钱类数据



float能代表的十进制 的最大精度小数点后7位
double 能代表的 十进制 的最大进度是小数点后15位

decimal能拥有更高的精度:28位

但是decimal的性能要比float/double慢很多.性能为后者的1/20

人类发明的任何概念,比如金融数据和比赛分数,适用于decimal
而其他的一些自然数据,当我们对精度要求不高的时候,可以使用float/double



#索引

组合主键

多字段组成的唯一索引



# 分表

水平分表

垂直分表





# int

##todo

int(11) 和int(10)的区别，大小并没有限制，只是自动填充0的区别

# 开销

* 衡量查询开销三个指标：响应时间、扫描的行数、返回的行数