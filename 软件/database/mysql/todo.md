把mysql的高可用，主从和双主的配置过程梳理一下    同mongo  redis



MyISAM 和INNODB  



MySQL数据库提供了四种隔离级别
a) Seriable（串行化）：可避免脏读、不可重复读、幻读的发生
b) Repeated read（可重复读）：可避免脏读、不可重复读的发生
c) Read committed（读已提交）：可避免脏读的发生
d) Read uncommitted（读未提交）：最低级别，任何情况都无法保证