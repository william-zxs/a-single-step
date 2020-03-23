#  docker

```
docker run -itd --name mymongo  imageId  -p 5000:5000
```

```
docker exec -it containerId /bin/bash
```

```
docker network ls 

```

如何组建局域网？ todo

#docker cp

docker cp  ./my.cnf  containerId:/etc/mysql/my.cnf



#环境变量

在Dockerfile 中定义

ENV  NODE_VERSION 7.2.0

在docker run 的时候注入 docker run  -e  NODE_VERSION 7.2.0

这两种方式定义的环境变量都会注入到容器env中

