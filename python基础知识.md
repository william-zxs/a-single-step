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





