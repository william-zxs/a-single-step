

#查看表的创建语句，使用引擎，字符集

```
show create table user;
```



#查看数据库的字符集情况

```
>SHOW VARIABLES WHERE Variable_name LIKE 'character_set_%' OR Variable_name LIKE 'collation%';



+--------------------------+----------------------------------------------------------+
| Variable_name            | Value                                                    |
+--------------------------+----------------------------------------------------------+
| character_set_client     | utf8                                                     |
| character_set_connection | utf8                                                     |
| character_set_database   | utf8mb4                                                  |
| character_set_filesystem | binary                                                   |
| character_set_results    | utf8                                                     |
| character_set_server     | utf8                                                     |
| character_set_system     | utf8                                                     |
| character_sets_dir       | /usr/local/Cellar/mysql@5.7/5.7.24/share/mysql/charsets/ |
| collation_connection     | utf8_general_ci                                          |
| collation_database       | utf8mb4_general_ci                                       |
| collation_server         | utf8_general_ci                                          |
+--------------------------+----------------------------------------------------------+
```

```
set character_set_connection = 'utf8mb4' （这是临时生效的，建议在配置中修改）
```

# case

```
1.简单Case函数写法(注意sex的位置)

select *,(CASE sex WHEN '1' THEN '男' WHEN '0' THEN '女' ELSE '保密' END) as sex_text
from user

2.Case搜索函数写法(注意sex的位置【推荐】)

select *,(CASE WHEN sex='1' THEN '男' WHEN sex='0' THEN '女' ELSE '保密' END) as sex_text
from user
```



# distinct

去除重复值

```sql
SELECT DISTINCT 列名称 FROM 表名称
```





# 笛卡尔积

了解笛卡尔积的影响和作用





#select count(1)

```
原理和区别
select count(1)
select count(*)
select count(主键)
```

