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

a.在Dockerfile 中定义

ENV  NODE_VERSION 7.2.0

b.在docker run 的时候注入

  docker run  -e  NODE_VERSION 7.2.0

  docker run  --env-file $PWD/env.sh

这两种方式定义的环境变量都会注入到容器env中



#Dockerfile

`Dockerfile` 构建分层存储的概念

