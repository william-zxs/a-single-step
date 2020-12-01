# mvn install

#mvn package



#mvn clean install -pl lottery-proto -am







#runtime

<scope>runtime</scope>





# mvnw



`mvnw`是Maven Wrapper的缩写。因为我们安装Maven时，默认情况下，系统所有项目都会使用全局安装的这个Maven版本。但是，对于某些项目来说，它可能必须使用某个特定的Maven版本，这个时候，就可以使用Maven Wrapper，它可以负责给这个特定的项目安装指定版本的Maven，而其他项目不受影响。

简单地说，Maven Wrapper就是给一个项目提供一个独立的，指定版本的Maven给它使用。



# 常用命令
**跳过单元测试**
```
mvn clean package -Dmaven.test.skip=true
```
**指定配置文件**
配置多配置文件后
```
mvn test -P test
mvn springboot:run -P dev
mvn clean package -P prod
```

**将配置更新到私服**
```
mvn clean deploy
```