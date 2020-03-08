# python基础知识

##深拷贝和浅拷贝

函数内部也可以改变全局变量

```
def demo(d):
		d['age']= 10
		
data = {'age':20}
demo(data)
>>>data
>>>{"age":10}
改变引用，就像tuple中的列表的值一样可以改变

```



```
todo
```

---

## python shell

PYTHONSTARTUP 环境变量

```shell
#!/bin/bash
export PYTHONSTARTUP=startup.py
python
```

```
PYTHONSTARTUP is an environment variable you will define specifying the location of the path to a python file
```

<PYTHONSTARTUP is an environment variable you will define specifying the location of the path to a python file>





## python2&python3比较

###路径差异:

绝对导入：跳过包内，直接搜索 sys.path ，在sys.path的基础上进行我们的模块搜索。

相对导入：先包内，再包外，再，，，

python2是默认相对导入的，因此对于一般性的导入，python2会进行如下搜索: 当前目录->上个目录->>根目录；sys.path路径，标准库，.pth文件

而python3是默认绝对导入的，因此python3直接跳过本包，直接到sys.path中寻找。

python3，python2目前都支持 . 相对路径， .. 根路径

为了更好的兼容性，请使用 . 或者 ..  表示本目录下面的内容引用。

### 编码

python2中默认编码方式是ascii

python3中默认编码方式是utf-8



python2中只有str类型，

python3中有str，bytes类型

```python3
sys.version_info[0]==3

In [29]: a = 'aaa'                                                                                                                                                                                                                         
In [30]: type(a)                                                                                                                                                                                                                            
Out[30]: str
In [31]: a.encode('utf-8')                                                                                                                                                                                                                  
Out[31]: b'aaa'
In [32]: type(a.encode('utf-8'))                                                                                                                                                                                                            
Out[32]: bytes
In [34]: m = a.encode('utf-8')                                                                                                                                                                                                              
In [35]: m                                                                                                                                                                                                                                  
Out[35]: b'aaa'
In [36]: m.decode('utf-8')                                                                                                                                                                                                                  
Out[36]: 'aaa'
In [37]: type(m.decode('utf-8'))                                                                                                                                                                                                            
Out[37]: str

In [39]: [x for x in m]                                                                                                                                                                                                                     
Out[39]: [97, 97, 97]
```

```
Python2 ｜	Python3 ｜	表现	｜ 转换 ｜	作用
str	bytes	字节	encode	存储
unicode	str	字符	decode	显示


```



| Python2 | Python3 | 表现 |  转换  | 作用 |
| :-----: | :-----: | :--: | :----: | :--: |
|   str   |  bytes  | 字节 | encode | 存储 |
| unicode |   str   | 字符 | decode | 显示 |