
做好面试二十次找到合适的工作的心态



分等级：
1.能百分百
2.大概率
3.小概率



语言：
java
golang
python


拼多多
一面

项目聊了20***要问到用的技术栈、中间件

Java 知识:

1. 异常体系设计
throwable ---》 error 和 exception
error 主要是程序无法处理的错误，jvm等异常，如 OOM
exception 是程序可以处理的错误分为runtime exception 和非运行时异常
    runtime exception 主要是 数组越界，空指针NullPointerException等异常，这些异常是不检查异常，程序中可以选择处理或者不处理，这些异常一般是由程序逻辑错误引起的， 
    程序应该从逻辑角度尽可能避免这类异常的发生。
    非运行时异常主要是 IO异常 ，从语法角度讲都是必须处理的异常，如果不处理程序就不能编译同通过，如IOException、SQLException等以及用户自定义的Exception异常，一般情况下不自定义检查异常。 

2. GC 过程，调优过程、死锁处理

3. 线程池设计，线程数量如何配置选择(高低并发、任务执行时间长以及短的各种场景)
https://www.jianshu.com/p/7726c70cdc40

如何配置线程池
CPU密集型任务
尽量使用较小的线程池，一般为CPU核心数+1。 因为CPU密集型任务使得CPU使用率很高，若开过多的线程数，会造成CPU过度切换。

IO密集型任务
可以使用稍大的线程池，一般为2*CPU核心数。 IO密集型任务CPU使用率并不高，因此可以让CPU在等待IO的时候有其他线程去处理别的任务，充分利用CPU时间。

Executors类提供了4种不同的线程池：newCachedThreadPool, newFixedThreadPool, newScheduledThreadPool, newSingleThreadExecutor


4. synchonized 和 lock 的实现，synchonized 底层实现、锁升级

操作系统:

1. 基础知识八股文，进程、线程的区别，线程同步、进程通信
进程是cpu分配资源的基本单位，线程是计算机调度的基本单位，一个进程里面至少有一个线程，同一进程内的线程共享本进程的资源，如内存、cpu、I/O,进程之间的资源是独立的，
多线程优点：对于i/o密集型的任务，多线程可以充分利用cpu，
多线程缺点：1.线程之间共享资源，线程之间的同步和加锁比较麻烦，2.同一进程内，一个线程崩溃可能会影响其他的线程的稳定性。3.上下文切换会给cpu增加负担。

多进程的优点：可以充分利用cpu的多核，资源相互独立，不用加锁，进程之间相互独立，稳定性比较好，通过增加cpu，可以极大的提高性能
多进程的缺点：通迅需要跨进程边界，如果需要传输大量数据，就不太好；进程调度开销也比较大
进程间的通讯方式：管道，半双工、单向流动，只能在父子进程间使用；
                命名管道，半双工，单向，可以在非亲缘关系的进程间使用；
                消息队列
                共享内存

2. 常用的 linux 命令

回答有用过ping、ssh，由此引发到计算机网络部分，ping、ssh 分别属于哪一

层，实现方式


cat  mv cp 
tar -zcvf  / -zxvf
scp  
grep -n -r 
rpm -ivh
ping 
telnet 
netstat
ll
du -sh
df -hl

网络七层：
https://blog.csdn.net/u011774517/article/details/67631439
物理层、数据链路层、网络层、传输层、会话层、表示层、应用层
物理层：定义了传输介质的特性，主要目的是透明的传输比特流，因为物理设备和传输媒体很多，物理层就是要屏蔽这些差异。
数据链路层：任务是在两个相邻的节点间毫无差错的传输以帧为单位的数据
网络层：主要的作用是寻址和路由
传输层：传输层的数据单位是报文，主要是一些针对报文的一些策略


物理层：中继器、集线器，以二进制的形式在无力媒介上传输数据
数据链路层：网桥，以太网交换机（二层交换机），网卡（一半是在数据链路层，一半是在物理层），以帧为单位保证无差错的传输数据

1层 物理层：
规定通信设备的机械的、电气的、功能的和过程的特性，用以建立、维护和拆除物理链路连接。具体地讲，机械 特性规定了网络连接时所需接插件的规格尺寸、引脚数量和排列情况等;电气特性规定了在物理连接上传输bit流时线路上信号电平的大小、阻抗匹配、传输速率 距离限制等;功能特性是指对各个信号先分配确切的信号含义，即定义了DTE和DCE之间各个线路的功能;规程特性定义了利用信号线进行bit流传输的一组 操作规程，是指在物理连接的建立、维护、交换信息是，DTE和DCE双放在各电路上的动作系列。在这一层，数据的单位称为比特(bit)。属于物理层定义的典型规范代表包括：EIA/TIA RS-232、EIA/TIA RS-449、V.35、RJ-45等。

2层 数据链路层：
在物理层提供比特流服务的基础上，建立相邻结点之间的数据链路，通过差错控制提供数据帧(Frame)在信道上无差错的传输，并进行各电路上的动作系列。数据链路层在不可靠的物理介质上提供可靠的传输。该层的作用包括：物理地址寻址、数据的成帧、流量控制、数据的检错、重发等。在这一层，数据的单位称为帧(frame)。数据链路层协议的代表包括：SDLC、HDLC、PPP、STP、帧中继等

3层 网络层：
在 计算机网络中进行通信的两个计算机之间可能会经过很多个数据链路，也可能还要经过很多通信子网。网络层的任务就是选择合适的网间路由和交换结点， 确保数据及时传送。网络层将数据链路层提供的帧组成数据包，包中封装有网络层包头，其中含有逻辑地址信息- -源站点和目的站点地址的网络地址。如 果你在谈论一个IP地址，那么你是在处理第3层的问题，这是“数据包”问题，而不是第2层的“帧”。IP是第3层问题的一部分，此外还有一些路由协议和地 址解析协议(ARP)。有关路由的一切事情都在这第3层处理。地址解析和路由是3层的重要目的。网络层还可以实现拥塞控制、网际互连等功能。在这一层，数据的单位称为数据包(packet)。网络层协议的代表包括：IP、IPX、RIP、OSPF等。

4层 传输层：
第4层的数据单元也称作数据包(packets)。但是，当你谈论TCP等具体的协议时又有特殊的叫法，TCP的数据单元称为段 (segments)而UDP协议的数据单元称为“数据报(datagrams)”。这个层负责获取全部信息，因此，它必须跟踪数据单元碎片、乱序到达的 数据包和其它在传输过程中可能发生的危险。第4层为上层提供端到端(最终用户到最终用户)的透明的、可靠的数据传输服务。所为透明的传输是指在通信过程中 传输层对上层屏蔽了通信传输系统的具体细节。传输层协议的代表包括：TCP、UDP、SPX等。

5层 会话层：
这一层也可以称为会晤层或对话层，在会话层及以上的高层次中，数据传送的单位不再另外命名，而是统称为报文。会话层不参与具体的传输，它提供包括访问验证和会话管理在内的建立和维护应用之间通信的机制。如服务器验证用户登录便是由会话层完成的。

6层 表示层：
这一层主要解决拥护信息的语法表示问题。它将欲交换的数据从适合于某一用户的抽象语法，转换为适合于OSI系统内部使用的传送语法。即提供格式化的表示和转换数据服务。数据的压缩和解压缩， 加密和解密等工作都由表示层负责。

7层 应用层：
应用层为操作系统或网络应用程序提供访问网络服务的接口。应用层协议的代表包括：Telnet、FTP、HTTP、SNMP等。





ping 和ssh属于应用层
ping 采用icmp协议

ssh 实现方式，
用户名密码登陆过程：ssh请求服务端，然后服务端会把自己的公钥发给客户端，客户端收到后会提示用户是否信任，点击yes之后会把公钥保存到known_hosts中，然后客户端把用户名和密码加密后传输给服务端，服务端收到后解析数据，连接成功。
公钥登陆：服务端将客户端的公钥保存在authorization_keys中，当客户端请求的时候服务端会给客户端一个字符串，客户端用私钥加密后发给服务端，服务端解密成功后，对比，如果正确则登陆成功。


计算机网络:

1. 三次握手和四次挥手
  1 客户端发送连接请求，
  2 服务端接受请求，返将序列号加1，返回序列号和连接请求
  3 客户端收到请求，建立连接，并返回服务端的序列号+1

2. 为什么握手是 3 次，两次可以吗，4 次呢

如果server 端没有收到第三次 ack，但是收到了 client 端发送的数据，server

端会怎么处理

3. 为什么挥手需要 4 次
因为服务端收到断开请求后会回复客户端确认，等到服务端处理完成之后，会向客户端发送断开请求
4. 介绍一下 tcp，如何保证可靠传输
https://zhuanlan.zhihu.com/p/112317245
a.三次握手、面向连接
b.超时重传，会根据传输时间 一来一回的时间来确定一个超时的时间，相同的数据会重新投递
c.拥塞控制，tcp有一个慢启动，数据传输量会有一个指数增长，摸清楚当前的网络拥堵状态后再决定按照多大的速度传输
滑动窗口控制，会连续发送多个消息，并缓存起来，如果客户端收到了就发送确认消息，服务端收到确认消息后就会从缓存中删除数据，如果某个数据丢失，服务端会收到某个应答包之后会再连续收到三次，只说明已经丢失了
d.最大消息长度
当建立tcp连接的时候，双方会约定一个最大的长度作为发送的单位，重传的时候也是按照这个单位重传


5. http 1/1.1/2 的区别

http1.1 比1.0 主要不同是使用了长连接，每一个连接可以多次使用，但是也是阻塞的。
http2 相比http1.1 多路复用，多个请求可以在一个连接上并行执行,把信息分为更小的帧，在应用层(HTTP/2)和传输层(TCP or UDP)之间增加一个二进制分帧层，在不改动 HTTP/1.x 的语义、方法、状态码、URI 以及首部字段的情况下, 解决了HTTP1.1 的性能限制，改进传输性能，实现低延迟和高吞吐量

httpget缓存问题

url 和 uri

6. https 相关问题

自签证书
http是明文传输的，https是通过ssl加密传输
整个加密过程是这样的：
首先客户端发起请求
服务端返回证书
客户端校验证书的有效期
然后从系统内置的公钥中找到ca的公钥，解密证书中的签名，然后再将证书的内容通过相同的摘要算法计算hash值，和解密的签名相比较，如果一致，则说明证书的信息没有被改变
然后客户端用服务端的公钥加密 对称加密的密钥 传输给服务端
服务端根据自己的私钥解密数据，获得对称加密的密钥
后面的传输都是通过对称加密的方式加密传输


https有两个作用，一个是身份认证、一个是数据加密

算法:

1. 手写单例模式

java设计模式
https://www.runoob.com/design-pattern/singleton-pattern.html
https://blog.csdn.net/mnb65482/article/details/80458571

单例的四大原则：
1.构造私有
2.以静态方法或者枚举返回实例
3.确保实例只有一个，尤其是多线程
4.确保反序列化时不会重新构建对象


饿汉式：
public class Singleton{

    privite static Singleton instance = new Singleton();
    privite Singleton(){}
    public static Singleton getInstance(){
        return instance;
    }
}

静态内部类：

```
当加载某个类的时候只能一个线程去加载 
```
public class Singleton{

    privite static class Inner(){
        private static final  Singleton instance = new Singleton();
    }

    privite Singleton(){}

    public static Singleton getInstance(){
        return Inner.instance;
    }
}

DCL： 要使用 volatile 防止 DCL失效问题，jvm存在乱序执行功能
public class Singleton(){
    privite volatile static Singleton instance = null;
    privite Singleton(){}
    public static getInstance(){
        if(instance == null){
            synchronized(Singleton.class){
                if(instance == null){
                    instance = new Singleton();
                }
            }
        }
        return instance

    }

}






2. 反转链表 leetcode 206

二面

项目经历聊了大概20min,比较关注项目经历中有难度、挑战的事情

最近的项目是中彩的纸质票项目，这个项目是全国的纸质票发行销售兑奖的一个系统，从票的印制计划、到交付中彩中心仓库、再到省市仓库、区县仓库、到站点、销售、兑奖。
微服务有  用户（角色、权限）、 账户、生产、游戏、调拨、销售、兑奖、异常票、仓库、通知、代理、网关、日汇总、报表、xxl-job

主要的微服务有  调拨、销售、兑奖、账户 四个最主要的微服务。 

我主要负责的是调拨、兑奖，生产和销售有一部分是

画一下架构图


算法:

1. 手写无锁队列

2. 遍历二叉树(非递归) leetcode 144

数据库:

1. 索引的实现方式
mysql innodb 的索引

2. hash、B+、B 树实现的优劣对比(Mysql MongoDB 分别是怎么实现的)

3. 数据库的事务、隔离级别、实现方式

开源社区: 日常工作中有没有参与经历过开源项目，看过什么源码，对该技术的理解

聊到了redis、kafka; redis 性能高效的原因(重新实现了数据结构、IO 多路复

用、多路复现的底层实现epoll，单线程基于内存)

持久化方式rdb、aof





58同城
1.自我介绍。
2.介绍一下项目，负责哪些模块，有看过源码吗？
3.currenthashMap和hashTable区别， 为什么线程安全的，hashmap1.7和1.8有什么区别。
4.HashMap为什么使用红黑树，是怎么扩容的，扩容时做了什么。
5.Jvm 分为哪些区域，运行时数据区又分为哪几个。
6.Mysql存储引擎，有什么区别，复杂的SQL一般怎么优化，
7.索引有哪些， user表中的性别添加索引会生效吗，使用like ， in, != (<>), or  索引有效吗，为什么使用B+tree，是怎么实现的
8.redis数据结构，redis的key过期会立即删除吗？
9.GC，引用计数和可达性分析，算法 标记清除，标记复制，标记整理
10.spring的IOC与AOP，哪些注解创建bean对象，springboot与spring区别，为什么使用SpringBoot
11.java8新特性


meituan

1、做一下自我介绍吧，简单说一下你的项目？

2、有遇到过内存泄漏吗？你们是怎么解决的？这个前阵子确实遇到过一次，还算运气比较好。
3、java的基本类型有哪几个？String是不是java的基本类型？String为什么要是final类型的？
4、反射机制的底层实现是什么？动态***呢？动态***的实现原理？
5、hashmap了解吗？说一下hashmap相关的一些东西？hashmap是线程安全的吗？为什么是线程安全的？concureenthashmap了解吗？他是如何实现线程安全的？你刚才说1.8基于cas？cas的ABA问题怎么解决？
6、说一下JVM的线程模型？这些区域都分别是干啥用的？java线程模型和jvm线程模型注意区分、总结下，网上很多文章都是错的。
7、说一下java类加载器的工作机制？类加载在那个区域进行的？
8、说一下java的线程模型？violate了解吗？他的原理是什么？violate是线程安全的吗？为什么不是？
9、保证线程安全的解决方法有哪些？说一说读写锁吧，读写锁的读
10、数据库的索引有哪几种？为什么要用B+树来做索引？组合索引和几个单个的索引有什么区别？数据库的大表查询优化了解吗？MVCC机制了解不？MVCC机制有什么问题？怎么去解决这个问题？mysql慢语句调优做过吗？说说你是怎么做的？
11、redis了解吗？你说说怎么用redis实现分布式锁？
12、spring中Bean的作用域，springMVC的controller是线程安全的吗？怎么去保证线程安全呢？





bilibili

一面
1.项目为什么要用消息队列？改成异步接口不行吗？
2.消息可靠性，消息重复消费。如果消息丢失，你应该怎么尽量地让用户觉得此次下单的

公平性？

3. Redis 性能为什么高？Redis的lua脚本，为什么能保证原子性？如果lua脚本在库存扣减

完以后执行出错怎么办？

4.项目如果要跟小公司进行对接，你会怎么做？

5. JVM 内存布局？GC算法？

6.请从操作系统以及CPU指令（怎么操作内存的）的角度去解释为什么会出现线程不安全？

（答不出来，cpu 指令不会..，扯开话题扯去JMM了）

7. http里面包含什么？

8. 两堆乱序扑克牌，要求合并成一堆有序的牌堆，怎么做？（归并+随便一个排序）时间复

杂度？

9.如果两堆1TB 的数据，要求合并成一堆有序的牌堆，怎么做？（归并+内部排序，分而治

之）

10.回到扑克牌的这个主题，要求把一堆乱序的扑克牌进行排序，如果要极致地压榨性能，

应该怎么做？时间复杂度能达到多少？

最后就是反问。


二面

1. UDP跟TCP的区别及场景？

2. Mysql三范式？为什么会有这三范式？

3. 缓存中间件了解吗？Redis，Memcache？（缓存中间件广度）Redis有多少种数据结构？

应用场景？为什么高性能？

4. zk了解吗？（注册中心广度）

5. kafka 了解吗？（mq广度）（介绍了卡夫卡在他们业务上的使用）

6.微服务设计思想？为什么需要这样设计？好处？

7.了解过Golang 吗？说说你的使用感受以及理解？



qu na

一面（50min）

除了项目之外是以下问题，其实项目问的是最多的了。

手撕代码：给定字符串，内部的单词用空格分隔，将其中的每个单词反转后输出字符串

手撕代码：给定字符串，内部的单词用空格分隔，去除其中重复的单词（即若后面有单词在

前面出现过，则删除后面的单词），并保持单词的原有顺序输出字符串。（用LinkedHashSet

即可）

Linux命令了解多少？查看内存占用？查看磁盘占用？查看某一端口？

谈谈SQL优化

手撕代码：快速排序，要求先说思路

二面（40min）

一面中的海盗分金币。你现在再想想看怎么做？（emm...）

一道编程题：象棋上马从一个位置跳到另一个位置最少需要跳多少次。你当时做出

来了，讲讲思路。（就是广度优先搜索）

BFS实现有个问题就是马在走的过程中其实有些方向其实是没必要考虑的，你有没更好的解

法？（那就启发式搜索，类似A*算法）

A*算法还不是最好的解，你有没更好的解？（emm...，其实面试官看到了一种解法很好，但

是我觉得很难想到，后面他就开始跟我讲什么要算根号五，算一堆啥的，然后再去重啥的，

我连忙点头，不过真没懂他在讲啥）

写SQL 代码：数据库表中有一列是姓名，一列是性别，如何建索引比较好

你觉得你的面试表现怎么样

HR面

期望薪资多少？最后给我薪资远低于我的预期，说你愿意考虑吗？问我为啥会离职之类的。



蘑菇街

问题：

聊10分钟项目

让你实现生产者消费者，类似阻塞队列那种的，你怎么实现？object类的notify和

wait+while循环

redis的常用数据结构以及使用场景。

mysql的是底层什么数据结构？为什么要B+树？

线程池，为什么要用线程池？满了怎么办？如果我想换个方式，改为满了之后先扩充最

大核心数呢？

双亲委派机制的过程？为什么要这个双亲委派机制？

netty？

问到了分表分库，假设有好多订单，现在分表分库了，我如何迅速找到我要的一堆数据。

· Map接口有哪些实现类

·讲一下LinkedHashMap？

·如何得到一个线程安全的Map？

· Java中有哪些锁？讲一下synchronized和ReentrantLock 的区别?

· Spring AOP是怎么实现的？

· JDK动态代理和CGLIB有什么区别？既然有没有实现接口都可以用CGLIB，为什么Spring

还要使用JDK动态代理？

· Spring AOP不能对哪些类进行增强？（没有被Spring管理的类，当时没想出来）

· Spring是怎么解决循环依赖的？多例对象之间的循环依赖？单例和多例之间的循环依

赖？

· MyBatis 中$和#的区别？既然$不安全，为什么还需要$，什么时候会用到它

· MySQL的ACID特性分别是怎么实现的？

· MySQL的事务隔离级别是怎么实现的？

·用过什么缓存框架？用过什么RPC框架？用过什么消息队列？

·除了Java自带的序列化之外，你还了解哪些序列化框架？

差不多就是这样了，相比其他公司的面试，感觉问的问题还是多的。






didi

1.介绍项目
2.介绍redis缓存，雪崩击穿等
3.redis执行原理，没明白猜测可能是数据结构map啥的。
4.ioc三级缓存
5.服务划分策略
6.dubbo底层协议
7.kafka 吞吐量，最大存储空间
8.问你项目数据量
9.线程池参数，怎么确定核心线程大小
10.cpu突然增大怎么排查，网络io突然增大呢。
11.fullgc怎么解决
12.rpc中使用事务该咋办


xiaohongshu

hashmap的底层数据结构，put的过程
hashmap是否是线程安全的，多线程下会有什么问题？concurrentHashMap底层是如何实现线程安全的。
synchronized锁的升级过程。
数据库是否用了索引？用explain无法看出索引用了哪一部分？
https://blog.csdn.net/houmenghu/article/details/109580196

遇到非等值判断时匹配停止

1
2
3
4
5
a = ? and b = ? and c= ?
a = ? and b = ? and c > ?
a = ? and b > ? and c > ?， 只用到索引的一部分(a,b)，因为b把数据阻断了，b不是定植时，c时无序的，无法使用(a,b,c)索引。
 
show global variables like 'optimizer_switch'\G
5.6版本后，可以开启索引下推。虽然有非等值条件，导致索引不能全部使用，但是可以利用索引条件，里面有的字段进行过滤，过滤后再回表读取真正的数据（extra=using index condition)，而不是只根据部分索引查出该索引符合条件的数据(回表数据太多，回表一般是随机io，减少回表次数)，然后再server层进行过滤，这样效率会很低(extra=using where)：

extra=using index是覆盖索引
type=index，表示使用索引排序

http://fivezh.github.io/2020/01/19/mysql-icp/?utm_source=tuicool&utm_medium=referral

spring循环引用的问题，A->B->A问题
spring对于单例模式，用了三级缓存
getBean(A)时，先实例化A，然后曝光到singletonFactories中，允许循环依赖。初始化结束后，再从提前曝光缓存earlySingletonObjects以及singletonFactories移除，挪到singletonOjbects单例缓存中。
getBean(B)依赖A，先在singletonObjects 中查找，如果有直接返回。如果不存在，在earlySingletonObjects中查找，这个是提前曝光，还未初始化的单例。如果不存在，在singletonFactories中查找，找到后放回earlySingletonObjects。这个时候A还没初始化。
举个不用回表的例子
覆盖索引

1
2
index (name, age)
select name,age from t where namg = "xiaoming";
主键用uuid会有什么问题？

聚蔟索引和非聚蔟索引的区别，是否分别对应主键索引、辅助索引？是的
https://www.jianshu.com/p/643850f684db
mysql索引，高度一般是3-4层，innodb的页大小是16kB，叶子节点是双向循环链表？一个b+树存储行数最多为2000w
https://zhuanlan.zhihu.com/p/86137284

实现LRUCache，这里可以考虑用map，节点是node，node之间通过前后指针关联，双向链表
https://leetcode-cn.com/problems/lru-cache/
存在个问题，一批新数据会把访问很久的数据给挤出去，这里如何解决这个问题？

https://juejin.cn/post/6844904049263771662

https://segmentfault.com/a/1190000038714624

jvm垃圾回收是如何做的？

jvm运行时有哪些数据区

哈希冲突如何解决

b+树叶子节点存的是指针吗？存的是数据

可重复读的情况下，select count(*) from t where a >= 0 and a <= 10在另一个事务执行前后效果如何？可重复读下，对于更新语句，会加锁。只不过是通过mvcc来实现可重复读，依然会出现幻读的现象，需要改为当前读
CMS和G1均使用三色标记法进行标记，一开始是白色对象。
黑色对象，自己和成员对象均已标记存活。
灰色对象，中间状态，自己存活，但是成员对象未标记（白色）
白色对象，未标记或者没有访问到（可以回收）
跨代引用
新生代引用老年代如何回收，直接扫描，因为新生代朝生暮死。
老年代引用新生代，回收新生代时minorgc，使用card table，牺牲空间换时间，减少扫描整个老年代的时间，因为老年代的存活时间是比较长的。https://www.jianshu.com/p/f1ff4ab0fed7，g1引入了remember set
write ahead log
https://martinfowler.com/articles/patterns-of-distributed-systems/wal.html
延迟关联，解决深分页问题
http://qidawu.github.io/2019/11/26/mysql-deferred-join/







最右APP 2技术1hr 已offer

一面
工作项目
比较有成就感的产出
redis相关,网络模型，存储模型，常用数据结构等
缓存穿透解决方案
分布式系统 CAP
工作项目中以及其他共识算法
raft算法细节（选主 复制 脑裂 balabala）
mysql索引相关，数据结构，优化，优缺点等
主键需要保证的特性以及为什么这样做
二面
场景题： 某个下游服务的接口并发量大应该如何解决？
给出了一个复用资源（池）的思路，
追问：引入池后会出现哪些问题，如何预防？
聊工作项目，很多问题基于项目问的
hr
1.聊人生



知乎 2技术1hr 已offer

一面

分布式系统一致性说一下
raft算法细节
锁问题，cas，锁的实践？
go标准库的 mutex介绍
bitcask存储模型细节，既然是追加写，那么如何做旧数据gc？重启后索引怎么恢复？
LSM tree介绍一下，相比b+ tree如何？
给TIDB代码贡献介绍一下，TIDB里query大概流程？
项目里的map并发怎么做？ 为啥用分段锁不用sync.map? 分段锁拆了几个分片？
内存对其了解吗？
简单介绍一下go的内存分配机制？ 有mcentral为啥要mcache？
答了 mcentral是服务所有系统线程，mcache为系统线程独享，mcache缺少span时去mcentral->mheap 中取
二面

聊了聊开源贡献
redis连环炮，数据结构+哨兵+同步
聊工作项目
innodb 连环炮 index redo undo mvcc
闲聊技术 人生 问了问组里的工作
hr

聊人生 聊发展
快手： 4轮技术1hr 口头offer 备胎

一面： （欢乐局
看你简历大学有竞赛经历，算法都懂吧？
我：了解
面试官：嗯，了解就不问了
raft算法懂不？
我： 懂
面试官：嗯，懂就不问了
讲讲tidb
讲讲newsql
项目吞吐量，怎么优化的性能？
工作有啥亮点？产出？ 共识怎么做的？
二面：（组长人超级nice！！！ 还帮忙问进度！！！
mmap操作原理
答： 1.内存映射 2.逻辑/物理地址转换 3. 程序访问触发缺页中断 4. 调页
追问：mmap的问题？
答了内存过大时会出现频繁的页面置换 影响效率
tidb项目介绍 sql parser做了啥？ planner做了啥？
讲 epoll
进程线程区别（刨根问底式
各种OS问题
虚拟内存， 缺页置换？ MMU？
写个代码 （忘了问啥了
三面：
项目介绍
设计一个kv存储
说一下你理解的共识算法
说一下多路复用
四面：
项目介绍
直接io与mmap区别？
分布式系统保证数据一致性？
redis主从怎么做的数据一致？
redis哨兵？
讲讲排序算法 优缺点
http连环问题 tcp连环问题 长链接短链接
http header 干啥用的？
写个代码 dijkstra模版题（用go写可真费劲
hr
大学做过自豪的事
一堆小问题
度小满 二面挂

一面：
linux命令
go性能调优怎么做的？
sql注入怎么防？
redis zset使用场景？
zset底层实现
跳表的细节？
go 中 sync.map
答： cas + dirty map + read map
打乱一个数组，不用rand
两个队列模拟栈
二面：
聊项目
没了
头条

一面：
写代码
如何做服务发现
微服务乱七八糟
写代码
二面：
写代码
没了
总结： 知乎面试体验最好，真的是在和求职者认真的沟通交流，发offer也是飞快，快手的技术面体验也不错，面试官会根据你擅长的方向来提出问题，不会张口闭口的微服务云原生，但是快手的hr真的一言难尽，给了口头offer提了工资流水以后发消息不回复，面试时间也给我排错了，人家面试官主动给我打的电话... 头条面试体验最差


shopee后端提前批一面二面hr面
一面7月11号     64分钟
自我介绍
讲下cms垃圾回收

cms第二个步骤是清理还是标记？

cms哪个步骤会stop the world

讲下https

数字证书原理

如果没有第三方我自己可不可以发布一个数字证书？

数字证书怎么验证的？

公钥和私钥？

非对称加密原理有了解吗？

公钥和私钥怎么生成的？

生成私钥的使用算法是什么？

你知道rsa吗？

mysql特性？隔离级别？

四种隔离级别的特点

mysql在哪个级别解决幻读问题的？

讲下间隙锁  加锁范围  具体说下

索引使用的数据结构

b+树和b树区别？

范围查询 b+树怎么实现的？

redis主从同步了解吗？

讲下redis数据类型

有序集合怎么实现的？

一致性哈希了解吗？

极限编程挑战赛做的什么？你做了什么？

你做出多少题？

软件精英挑战赛做了什么？

100万 0到1万随机乱序数，o(n)下，找中位数

算法题: 最长公共子串 （耗时22分钟）十分钟思考 12分钟写

反问

二 面7月18号     58分钟
自我介绍
看你有实习经历，介绍下

实习的公司做啥的

项目中你具体做的什么？

订单表怎么实现的？

订单id怎么生成的？

表的主键是什么？

为什么要做软删除？

订单id除了自增主键还有什么生成方式？

项目上线了没有？用户量怎么样？

sql运行过程？详细点

缓存的原理是什么？

mysql对sql语句怎么优化的？

你刚刚提到哈希表，聊聊哈希表数据结构和实现原理

算法题： 有三个子节点的树的层序遍历，并且实现测试用例编写和测试输出。  这道题半小时写完，既写层序遍历，还需要手写测试用例。

你自己的职业规划

你去年参加过shopee面试？

反问

hr面7月23号    25分钟
自我介绍

先确认本科研究生学历，什么时候毕业，能不能拿到双证

在学校成绩怎么样？ 排名

研究生研究方向

为什么没选算法选择后端呢？

介绍下项目

项目中遇到的挑战 怎么解决的

后期有没有优化改进？

做项目有人带你吗 还是自己从0到1的？

怎么学习这些知识的呢？

挑选公司最看重什么？ 优先级列三点

对我们公司的了解

有拿到哪些offer?或者还有哪些在流程中？

将来阿里 腾讯 字节会投吗？ 会去吗？

反问





## 其他

跨域

由于浏览器的同源策略
协议、域名（或ip）、端口 如果不一致的话，无法请求资源

解决方法：
CORS 跨域资源分享  这种方式比较老了，而且也不是太安全
方式：服务端设置 Access-Control-Allow-Origin，允许跨域请求
     客户端需要配置

现在的解决方案：
https://www.cnblogs.com/wasbg/p/10973880.html
前端 vue开发环境，在配置中配置proxytable
生产环境配置nginx代理，将请求的path 转发到相应的服务







GET、POST区别
get一般用来查询东西，有些缓存是按照get 的uri来标示的，get请求不建议携带body数据，因为很多老版本的客户端都是不会发送body数据的，而且body数据也会让缓存失效
post一般用来创建数据、修改状态

浏览器缓存机制、304 缓存击中


HTTP1.x的解析是基于文本



java基础知识、JVM

spring 专题

项目


synchronized(this){}




访问百度的步骤


小米java开发二面面经

* 切面可能失效的原因
AOP实现的方式：
通过jdk动态代理
CGLIB
如果被代理的目标对象实现了至少一个接口，则会使用JDK动态代理。所有该目标类型实现的接口都将被代理。 若该目标对象没有实现任何接口，则创建一个CGLIB代理。
失效的原因：
1. 内部调用
一个切面方法和调用同一个类内的另一个切面方法，则第二个就不会生效
可以通过 AopContext.currentProxy().method2() 来调用
@Transactional  同样也有这个问题

* 慢sql问题定位
先查慢sql日志，找到相应的sql
查看sql是否使用了索引，简单的就是通过看sql使用的字段和ddl，如果没有，就加上索引
如果有，看一下explain 是否真正的使用过了索引。
这仅仅是软件层面，还要看看是否是硬件不够了，配置项如连接数之类的。

* mysql存储引擎的区别
我们常用的就是 innodb，支持事务，存储结构使用的是B+tree
 InnoDB是聚集索引，使用B+Tree作为索引结构，数据文件是和（主键）索引绑在一起的（表数据文件本身就是按B+Tree组织的一个索引结构），必须要有主键，通过主键索引效率很高。但是辅助索引需要两次查询，先查询到主键，然后再通过主键查询到数据。因此，主键不应该过大，因为主键太大，其他索引也都会很大。


innodb支持表 和行锁，myisam 支持表锁
InnoDB的行锁是实现在索引上的，而不是锁在物理行记录上。潜台词是，如果访问没有命中索引，也无法使用行锁，将要退化为表锁。

InnoDB为什么推荐使用自增ID作为主键？
自增ID可以保证每次插入时B+索引是从右边扩展的，可以避免B+树和频繁合并和分裂（对比使用UUID）。如果使用字符串主键和随机主键，会使得数据随机插入，效率比较差。

InnoDB：
1. 数据文件本身就是索引文件
2. 表数据文件本身就是按B+Tree组织的一个索引结构文件
3. 聚集索引中叶节点包含了完整的数据记录
4. InnoDB表必须要有主键，并且推荐使用整型自增主键

几种树的不同

操作系统储存数据的最小单位是页（page），一页假设是4K大小（由操作系统决定）


1.innodb支持事务、myisam不支持
2.innodb支持表锁、行锁，myisam只支持表锁
3.innodb聚簇索引的叶子结点保存了数据，myisam保存了数据的地址

* ACID
A:原子性
指同一个事务里的操作要么同时成功、要么同时失败。
C:一致性
数据库的完整性和一致性，一个事务执行之前和执行之后数据库都处于一致性状态
I:隔离性
是指各个事务之间通过一定的隔离级别相互隔离，进行一个并发控制
D:持久性
是指事务提交后就会保存在磁盘里
一旦事务提交，那么它对数据库中的对应数据的状态的变更就会永久保存到数据库中

隔离级别，以及相应的问题：

读未提交
一个事务可以读取到另一个事务修改但是还没提交的数据
存在的问题就是会脏读

读已提交
一个事务会读取另一个事务已经提交的数据。
存在的问题是 不可重复读，前后两次读取的数据不相等

可重复读
是指在一个事务里可以重复读取数据，不受其他事务影响
会存在幻读，select * from tb where id >10  insert tb id (11)可能会出错，因为11存在了

解决方式是 加上 for update 这样就会加上间隙锁，

串行化
事务的查询会加共享锁，提交后才会释放。死锁的概率很高，所以也不长用。

在可重复读的隔离级别下，要想避免幻读，可以用共享锁 lock in share mode 、或者for update锁住范围，这样就会加上间隙锁。


* MVCC机制

* B+树具体实现
B+Tree 每个节点有多个Key和Data， 子节点不保存数据，只保存索引，

* 千万数据在MYSQL的B+树上会存几层
三层

磁盘读取的单位是扇区大概是512Bytes，操作系统一次读取4kb，mysql一般一个节点大概是4kb
假设一个索引是10Bytes，那么一节点大概就是400个索引，400*400*400 = 64000000 大概就是6千万数据
一般根节点要常驻内存，所以只需要io两次就可以了



* MYSQL有哪些日志？都有什么用
redo log
redo log包括两部分：一是内存中的日志缓冲(redo log buffer)，该部分日志是易失性的；二是磁盘上的重做日志文件(redo log file)，该部分日志是持久的。
用来保证事务的持久性，指事务提交，服务器宕机，重启后会根据redo log 来恢复磁盘脏页
redo log的刷盘：
1. 每隔一秒会有一个刷盘动作
2. 每个事务提交时会将重做日志刷新到重做日志文件
3. 当重做日志缓存空间小于一半的时候，会刷新到缓存文件


undo log
Undo log是InnoDB MVCC事务特性的重要组成部分
当rollback将数据恢复到原始之前类似于备份表,为了保证事务的原子性
Innodb使用undo log实现mvcc,从undo log读取旧版本的数据

bin log
记录逻辑日志，sql和反向sql，用于主从复制
刷盘策略：
1. sync_binlog=0 每次事务提交都写到文件，文件的刷盘靠文件系统
2. sync_binlog=N N次事务提交触发一次binlog写入文件系统并调用fdatasync()刷盘


bin log 和 undo log、redo log的区别
1. 处理层次不同，REDO/UNDO LOG由Innodb存储引擎处理，而BINLOG由MySQL 服务层处理
2. 记录内容不同，REDO/UNDO LOG记录的数据页的修改情况，REDO LOG采用物理日志+逻辑日志的方式存储，UNDO LOG采用逻辑日志方式存储，用于保证数据一致性；而BINLOG日志记录的事务操作的内容，用于主从复制。
3. 记录时机不同，REDO/UNDO LOG在事务的执行过程中不断生成和写入，而BINLOG在事务最终COMMIT前写入。

慢查询日志



* mysql执行流程
https://blog.csdn.net/weixin_29477915/article/details/113199746
mysql主要分为server和存储引擎层
server层：连接器、查询缓存、分析器、优化器、执行器，还有一个日志模块binlog，这个日志模块所有的引擎都可以使用

存储引擎层：innodb,myisam,memory

查询执行过程：权限校验、查询缓存、分析器、优化器、权限校验、执行器、引擎
更新执行过程：分析器、权限校验、执行器、引擎、redo log prepare、binlog、redo log commit









* common-pool2
配置：
maxTotal: 对象池中最多允许的对象数，默认8
maxIdle: 对象池中最多允许存在的空闲对象，默认8
minIdle: 池中最少要保留的对象数，默认0
lifo: 是否使用FIFO先进先出的模式获取对象（空闲对象都在一个队列中），默认为true使用先进先出，false是先进后出
fairness: 是否使用公平锁，默认false(公平锁是线程安全中的概念，true的含义是谁先等待获取锁，随先在锁释放的时候获取锁，如非必要，一般不使用公平锁，会影响性能)
maxWaitMillis：从池中获取一个对象最长的等待时间，默认-1，含义是无限等，超过这个时间还未获取空闲对象，就会抛出异常。
minEvictableIdleTimeMillis：最小的驱逐时间，单位毫秒，默认30分钟。这个用于驱逐线程，对象空闲时间超过这个时间，意味着此时系统不忙碌，会减少对象数量。
evictorShutdownTimeoutMillis：驱逐线程关闭的超时时间，默认10秒。
softMinEvictableIdleTimeMillis：也是最小的驱逐时间，但是会和另一个指标minIdle一同使用，满足空闲时间超过这个设置，且当前空闲数量比设置的minIdle要大，会销毁该对象。所以，通常该值设置的比minEvictableIdleTimeMillis要小。
numTestsPerEvictionRun: 驱逐线程运行每次测试的对象数量，默认3个。驱逐线程就是用来检查对象空闲状态，通过设置的对象数量等参数，保持对象的活跃度和数量，其是一个定时任务，每次不是检查所有的对象，而是抽查几个，这个就是用于抽查。
evictionPolicyClassName: 驱逐线程使用的策略类名，之前的minEvictableIdleTimeMillis和softMinEvictableIdleTimeMillis就是默认策略DefaultEvictionPolicy的实现，可以自己实现策略。
testOnCreate: 在创建对象的时候是否检测对象，默认false。后续会结合代码说明是如何检测的。
testOnBorrow: 在获取空闲对象的时候是否检测对象是否有效，默认false。这个通常会设置成true，一般希望获取一个可用有效的对象吧。
testOnReturn: 在使用完对象放回池中时是否检测对象是否仍有效，默认false。
testWhileIdle: 在空闲的时候是否检测对象是否有效，这个发生在驱逐线程执行时。
timeBetweenEvictionRunsMillis: 驱逐线程的执行周期，上面说过该线程是个定时任务。默认-1，即不开启驱逐线程，所以与之相关的参数是没有作用的。
blockWhenExhausted: 在对象池耗尽时是否阻塞，默认true。false的话超时就没有作用了。


TimeBetweenEvictionRunsMillis
当TimeBetweenEvictionRunsMillis大于0时，会启动驱逐线程，定时执行驱逐。
先是判断池是开启状态，且空闲对象要大于0，不然不需要驱逐，每次会尝试驱逐numTestsPerEvictionRun（默认3个）个对象，当任务执行后后会判断是否小于minIdel，小于则创建足够的对象，直到idel数量等于minIdel。根据DefaultEvictionPolicy来校验驱逐策略，如果是驱逐，调用destory销毁对象。否则，判断testWhileIdle配置项，决定是否校验对象是否可用，先激活对象activateObject，有问题则直接销毁。否则校验对象可用性validateObject，失败则销毁，成功就钝化变成原样子。



common-pool2工作逻辑：

我们首先要创建一个 GenericObjectPool 池，参数是池管理的对象的工厂对象（实现PooledObjectFactory接口）。池主要做对象的管理工作，借、还、检查有效性、创建新对象、销毁对象。池对象工厂用来实现池对象的生命周期方法，创建、销毁、校验、激活、钝化

借对象：先去池里面从idle中获取一个，没有的话就创建一个，如果超过maxTotal，返回null，创建失败线程阻塞，等待时间如果是-1就一直等待，不是-1到指定时间还没等到就抛出异常，不等待会在没有获取到对象的时候直接抛出异常，获取后激活对象，失败就销毁，成功后判断borrow和create的时候校验可用性，失败则销毁。

还对象：还的时候判断是否要校验可用性，如校验不可用则销毁，之后钝化对象，失败则销毁，超过maxIdle也直接销毁


涉及销毁对象，所以都要进行确定minidle来决定是否补充对象。



* 分布式事务解决方案
https://xiaomi-info.github.io/2020/01/02/distributed-transaction/

ACID 刚性事务

分布式环境：柔性事务


XA:两阶段提交

TCC: try confirm cancel

两阶段提交和TCC还是比较像的，但是两阶段提交会有一个事务管理器，而TCC是由主事务发起


可靠消息最终一致性:

尽最大努力通知:



中间件：
seata



saga模式



* 分布式锁

基于redis 的分布式锁








* 对象池 common pool2
https://juejin.cn/post/6956383016469921822
配置：
maxTotal: 对象池中最多允许的对象数，默认8
maxIdle: 对象池中最多允许存在的空闲对象，默认8
minIdle: 池中最少要保留的对象数，默认0
lifo: 是否使用FIFO先进先出的模式获取对象（空闲对象都在一个队列中），默认为true使用先进先出，false是先进后出
fairness: 是否使用公平锁，默认false(公平锁是线程安全中的概念，true的含义是谁先等待获取锁，随先在锁释放的时候获取锁，如非必要，一般不使用公平锁，会影响性能)
maxWaitMillis：从池中获取一个对象最长的等待时间，默认-1，含义是无限等，超过这个时间还未获取空闲对象，就会抛出异常。
minEvictableIdleTimeMillis：最小的驱逐时间，单位毫秒，默认30分钟。这个用于驱逐线程，对象空闲时间超过这个时间，意味着此时系统不忙碌，会减少对象数量。
evictorShutdownTimeoutMillis：驱逐线程关闭的超时时间，默认10秒。
softMinEvictableIdleTimeMillis：也是最小的驱逐时间，但是会和另一个指标minIdle一同使用，满足空闲时间超过这个设置，且当前空闲数量比设置的minIdle要大，会销毁该对象。所以，通常该值设置的比minEvictableIdleTimeMillis要小。
numTestsPerEvictionRun: 驱逐线程运行每次测试的对象数量，默认3个。驱逐线程就是用来检查对象空闲状态，通过设置的对象数量等参数，保持对象的活跃度和数量，其是一个定时任务，每次不是检查所有的对象，而是抽查几个，这个就是用于抽查。
evictionPolicyClassName: 驱逐线程使用的策略类名，之前的minEvictableIdleTimeMillis和softMinEvictableIdleTimeMillis就是默认策略DefaultEvictionPolicy的实现，可以自己实现策略。
testOnCreate: 在创建对象的时候是否检测对象，默认false。后续会结合代码说明是如何检测的。
testOnBorrow: 在获取空闲对象的时候是否检测对象是否有效，默认false。这个通常会设置成true，一般希望获取一个可用有效的对象吧。
testOnReturn: 在使用完对象放回池中时是否检测对象是否仍有效，默认false。
testWhileIdle: 在空闲的时候是否检测对象是否有效，这个发生在驱逐线程执行时。
timeBetweenEvictionRunsMillis: 驱逐线程的执行周期，上面说过该线程是个定时任务。默认-1，即不开启驱逐线程，所以与之相关的参数是没有作用的。
blockWhenExhausted: 在对象池耗尽时是否阻塞，默认true。false的话超时就没有作用了。


TimeBetweenEvictionRunsMillis
当TimeBetweenEvictionRunsMillis大于0时，会启动驱逐线程，定时执行驱逐。
先是判断池是开启状态，且空闲对象要大于0，不然不需要驱逐，每次会尝试驱逐numTestsPerEvictionRun（默认3个）个对象，当任务执行后后会判断是否小于minIdel，小于则创建足够的对象，直到idel数量等于minIdel。根据DefaultEvictionPolicy来校验驱逐策略，如果是驱逐，调用destory销毁对象。否则，判断testWhileIdle配置项，决定是否校验对象是否可用，先激活对象activateObject，有问题则直接销毁。否则校验对象可用性validateObject，失败则销毁，成功就钝化变成原样子。


common-pool2工作逻辑：

我们首先要创建一个 GenericObjectPool 池，参数是池管理的对象的工厂对象（实现PooledObjectFactory接口）。池主要做对象的管理工作，借、还、检查有效性、创建新对象、销毁对象。池对象工厂用来实现池对象的生命周期方法，创建、销毁、校验、激活、钝化

借对象：先去池里面从idle中获取一个，没有的话就创建一个，如果超过maxTotal，返回null，创建失败线程阻塞，等待时间如果是-1就一直等待，不是-1到指定时间还没等到就抛出异常，不等待会在没有获取到对象的时候直接抛出异常，获取后激活对象，失败就销毁，成功后判断borrow和create的时候校验可用性，失败则销毁。

还对象：还的时候判断是否要校验可用性，如校验不可用则销毁，之后钝化对象，失败则销毁，超过maxIdle也直接销毁

涉及销毁对象，所以都要进行确定minidle来决定是否补充对象。




* mysql查询死锁

mysql磁盘慢了之后会导致锁库了

查询数据库中表的状态，是否被锁

SHOW FULL PROCESSLIST
查询的是information_schema.processist;
查询出来的id是线程id，可以通过 kill id 来杀掉线程

information_schema.innodb_trx;
information_schema.innodb_locks;

查看正在锁的事务
SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCKS; 
查看等待锁的事务
SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCK_WAITS;


