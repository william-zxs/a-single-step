# python基础知识

## python语言类型

python是强类型动态语言

```
强类型  如 java python c
1+'1'
error
弱类型  如 js php
1+ ‘1’
‘11’
```

```
x + y 

在代码执行前并不知道x 和y是什么类型的数据

静态语言 c/c++ java  c#
动态语言 python  js  ruby php
```







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





## dict

###setdefault

存在就返回存在的值（存在None就返回None），不存在就创建新的key-value加进去

```python

>>>a = {"name":"william"}
>>>a.setdefault("age",20)
>>>{"name":"william","age":20}

```



## 装饰器

demo

```python
# coding=utf8

def create_pro(fun):   #creapro = get_conns(fun) = ini
    def ini_fun(*args, **kw):
        if not isinstance(args[0], type(create_pro)):
            print(args)
            print('创建属性')
            return fun(*args, **kw)
        return fun(*args, **kw)
    return ini_fun


@create_pro
def create_vertex(fun):

    def dowork(args):
        print(args)
        print('创建顶点')

    if not isinstance(fun, type(create_vertex)):
        dowork(fun)
    else:
        def ini_fn(*args, **kw):
            dowork(args)
            return fun(*args, **kw)
        return ini_fn

@create_pro
@create_vertex
def create_edge(conn_id):
    print('创建边')
    return conn_id

if __name__ == '__main__':

    create_edge(1)
    # create_vertex(1)
```



### class

@staticmethod

@classmethod

```
e.g.
class Dog(object):
		def __init__(self,name):
				self.name = name
		@classmethod
		def color():
				return 'yellow'
		@staticmethod
		def age():
				return 5

```

---



```
from __future__ import absolute_import, unicode_literals
```

```
sys.setdefaultencoding
python3中不会存在
UnicodeDecodeError: 'ascii' codec can't decode byte 0xe9 in position 0: ordinal not in range(128)
Attempted relative import in non-package

UnicodeDecodeError: 'utf8' codec can't decode byte 0x9c in position 1: invalid start byte
```

