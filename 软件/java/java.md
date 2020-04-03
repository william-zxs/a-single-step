#javac

将.java文件编译成字节码 .class文件



思乐面试题中的概念。





final

interface

接口和抽象类



#限定符

protected

private

public

无（默认）

|   修饰词   | 本类 | 同一个包的类 | 继承类 | 其他类 |
| :--------: | :--: | :----------: | :----: | :----: |
|  privite   |  Y   |      X       |   X    |   X    |
| 无（默认） |  Y   |      Y       |   X    |   X    |
| protected  |  Y   |      Y       |   Y    |   X    |
|   public   |  Y   |      Y       |   Y    |   Y    |





#三元

```java
start = start < 0 ? 0:start;
```



#interface 

implements 实现接口，可以实现多个接口



#abstract

extends 继承类





#构造方法

1 调用子类构造函数的时候，会默认先调用父类的无参数构造方法，即相当于隐藏了一行代码 super();

2.在你程序没有写构造方法时候，编译器会默认帮你写一个无参数的构造方法，只不过方法里面没有内容
然而当你编写了构造函数的话，编译器就不会再帮你添加无参数的构造方法了，即使你只编写了有参数的构造方法。
如果你已经写了一个有参数的构造函数，并且你需要一个没有参数的构造函数，你必须自己动手写。
只要你有自己写的构造函数，不管是哪一种，这都会想是在跟编译器说：老兄，我自己的构造函数不用你管



#文件命名

JAVA语言，有严格的大小写区分。

JAVA源文件名必须符合以下规则：

1、必须以.java结尾。这样才能被编辑器javac.exe所编辑。

2、源文件中如果只有一个类，文件名必须与该类名相同。

3、如果有多个类，且没有public类，文件名可与任一类名相同。

4、有多个类，且有public类，文件名必须与该类名相同。

 注：**一个JAVA源文件只能有一个public类。一个文件中只能有一个main主函数**



#静态域、静态常量、静态方法

静态域
如果将类中的域定义为static，则这个域属于这个类，而不属于这个类的某个对象，每个类中只有一个这样的域，而每一个类对象对于所有的实例域(即没有定义为static的域)都有自己的一份拷贝。

例如：

class Employee
{
    ……
    private int id;
    private static int nextId = 1;
}
1
2
3
4
5
6
如果有1000个Employee对象，则有1000个实例域id，但是只有一个静态域nextId；即使没有一个Employee对象，静态域nextId也存在，它属于类，不属于任何对象。（所有的对象引用的静态变量都是同一个）
静态域也称为类域。

静态常量
如果一个域被定义为static final，则这个域就是一个静态常量。不能省略任何一个关键字，若是少了static，则该域变成了一个实例域，需要由类对象对其进行访问。若是省略了final，则该域变成了静态域，静态方法可以对其进行修改。

例子：

public class Math
{
    ……
    public static final double PI=3.14159265358979323864；
    ……
}
1
2
3
4
5
6
其中PI就是一个静态常量。

静态方法
静态方法是一种不能向对象实施操作的方法。Math的pow方法就是一个静态方法，在运算时，不使用任何Math对象，换句话说，没有隐式的参数this。因为静态方法不能操作对象，所以不能在静态方法中访问实例域，但是静态方法可以访问自身类中的静态域。可以使用对象调用静态方法，但是这样容易引起混淆，因为计算的结果与对象毫无关系，建议还是使用类名，而不是类对象调用静态方法。

例如：

public static int getNextId( )
{
    return nextId；
}
1
2
3
4
但是，如果去掉其中的关键字static，它就成了非静态方法，但是也可以访问类中的静态域，这时就需要由该类的对象来调用该函数。

在下面两种情况下使用静态方法：

1.一个方法不需要访问对象的状态，其所需的参数都是通过显式的提供

2.一个方法只需访问类的静态域

# 枚举

enum

除了枚举常量外, enum是一个完整的类,它也可以编写自己的构造方法以及方法,甚至实现接口.

枚举类不能继承其他类,因为在编译时它已经继承了 `Enum`



# 范型

类型参数<T>    无界通配符 <?>

有界通配符<? extends XXX>    <? super XXX>



标记符含义**

 **E** - Element (在集合中使用，因为集合中存放的是元素)

 **T** - Type（Java 类）

 **K** - Key（键）

 **V** - Value（值）

 **N** - Number（数值类型）



#匿名函数

lambda函数  箭头函数

e.g.

```
@Bean
public GlobalClientInterceptorConfigurer globalInterceptorConfigurerAdapter() {
    return registry -> registry.addClientInterceptors(new LogGrpcInterceptor());
}
```



#单双引号

区别1：java中的[单引号](https://www.baidu.com/s?wd=单引号&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)表示字符，java中的[双引号](https://www.baidu.com/s?wd=双引号&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)是字符串。

区别2：[单引号](https://www.baidu.com/s?wd=单引号&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)引的数据一般是char类型的；[双引号](https://www.baidu.com/s?wd=双引号&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)引的数据 是String类型的。

区别3：java中[单引号](https://www.baidu.com/s?wd=单引号&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)里面只能放一个字母或数字或符号；java中的[双引号](https://www.baidu.com/s?wd=双引号&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)里面是0到多个字符构成。所以字符可以直接转换成字符串。字符串需要使用charAt（n) 来获取第几个字符。

char定义时用单引号，只能有一个字母，数字。char c='c'；而String用双引号，可以是一个，也可能是多个字母，汉字等。就是所谓的字符串。String s="adsaf";

char只是一个基本类型，而String 可以是一个类，可以直接引用。比如char c='c';不能直接对c调用方法。String s="abc";  这时可以调用s.charAt(0);等方法,因为String是类，这是就是对象的调用了