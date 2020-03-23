#mongoDB

## 安装

```
http://www.cnblogs.com/kevingrace/p/5752382.html
```



##副本集

```
https://cloud.tencent.com/developer/article/1026185
```



副本集可以是两个节点吗？

“不可行,mongodb要求副本集必须是3个及以上的奇数节点,2个节点没法选举出leader,会导致你的集群一直处于不可用状态。”

```javascript
Mongodb一共有三种集群搭建的方式：
Replica Set（副本集）
Sharding（切片）
Master-Slaver（主从）【目前已不推荐使用了！！！】

其中，Sharding集群也是三种集群中最复杂的。
副本集比起主从可以实现故障转移！！非常使用！

mongoDB目前已不推荐使用主从模式，取而代之的是副本集模式。副本集其实一种互为主从的关系，可理解为主主。
副本集指将数据复制，多份保存，不同服务器保存同一份数据，在出现故障时自动切换。对应的是数据冗余、备份、镜像、读写分离、高可用性等关键词；
而分片则指为处理大量数据，将数据分开存储，不同服务器保存不同的数据，它们的数据总和即为整个数据集。追求的是高性能。

在生产环境中，通常是这两种技术结合使用，分片+副本集。
```

MongoDB的副本集 是自带故障转移功能的主从复制



```

community:PRIMARY> rs.status()
{
	"set" : "community",
	"date" : ISODate("2020-03-12T07:44:48.804Z"),
	"myState" : 1,
	"term" : NumberLong(2),
	"heartbeatIntervalMillis" : NumberLong(2000),
	"members" : [
		{
			"_id" : 0,
			"name" : "192.168.0.10:32780",
			"health" : 1,
			"state" : 2,
			"stateStr" : "SECONDARY",
			"uptime" : 93,
			"optime" : {
				"ts" : Timestamp(1583999000, 2),
				"t" : NumberLong(2)
			},
			"optimeDate" : ISODate("2020-03-12T07:43:20Z"),
			"lastHeartbeat" : ISODate("2020-03-12T07:44:46.858Z"),
			"lastHeartbeatRecv" : ISODate("2020-03-12T07:44:48.386Z"),
			"pingMs" : NumberLong(1),
			"syncingTo" : "192.168.0.11:32771",
			"configVersion" : 32920
		},
		{
			"_id" : 1,
			"name" : "192.168.0.11:32771",
			"health" : 1,
			"state" : 1,
			"stateStr" : "PRIMARY",
			"uptime" : 13335,
			"optime" : {
				"ts" : Timestamp(1583999000, 2),
				"t" : NumberLong(2)
			},
			"optimeDate" : ISODate("2020-03-12T07:43:20Z"),
			"infoMessage" : "could not find member to sync from",
			"electionTime" : Timestamp(1583999000, 1),
			"electionDate" : ISODate("2020-03-12T07:43:20Z"),
			"configVersion" : 32920,
			"self" : true
		}
	],
	"ok" : 1
}


-------
state 值越小，权重越高



```







### 配置副本集

```
https://cloud.tencent.com/developer/article/1026185
```



```javascript
MongoDB 安装目录:/usr/local/mongodb
MongoDB 数据库目录:/usr/local/mongodb/data
MongoDB 日志目录:/usr/local/mongodb/log/mongo.log 
MongoDB 配置文件:/usr/local/mongodb/mongodb.conf
```







---

##使用js函数  funciton  

```
> function add(){var i = 0;for(;i<20;i++){db.persons.insert({"name":"wang"+i})}}
> add()
```

---

## 主从

mongo.conf

```
master：默认为false，当设置为true，则配置当前实例作为主节点。
slave：默认为false，当设置为true，则配置当前实例作为从节点。
source：默认为空，用于从节点，指定从节点的复制来源（主节点的IP+端口），格式为：<host><:port>
only：默认为空，用于从节点，主动复制默认复制主节点上所有的数据库，通过设置此项指定需要复制的数据库名称
slavedelay：设置从库同步主库的延迟时间，用于从设置，默认为0，单位秒。
autoresync：默认为false，用于从设置。是否自动重新同步。设置为true，如果落后主超过10秒，会强制从自动重新同步。如果oplogSize太小，此设置可能有问题。如果OPLOG大小不足以存储主的变化状态和从的状态变化之间的差异，这种情况下强制重新同步是不必要的。当设置autoresync选项设置为false，10分钟内从不会进行大于1次的自动重新同步
```



## $lookup

多表关联查询