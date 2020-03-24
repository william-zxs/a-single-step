from 

COPY

RUN

EXPOSE

ENTRYPOINT

CMD

挂载目录











```shell
from docker.io/centos:8
MAINTAINER William-ZXS
RUN yum clean all
RUN yum install -y redis
RUN yum clean all
# RUN yum install -y redis && rm -f /var/lib/rpm/__db* && rpm --rebuilddb && yum clean all
RUN sed -i 's/^bind/#bind/' /etc/redis.conf
RUN sed -i 's/^daemonize yes/daemonize no/' /etc/redis.conf
RUN sed -i 's/^protected-mode yes/protected-mode no/' /etc/redis.conf

EXPOSE 6379

ENTRYPOINT ["/usr/bin/redis-server"]
CMD ["/etc/redis.conf"]
```





```shell

from docker.io/centos:8

RUN yum install -y redis  && yum clean all

COPY init.sh /usr/local/bin/
RUN ln -s usr/local/bin/init.sh / 
RUN sed -i -e 's/^bind[ ]*127.0.0.1/bind 0.0.0.0/' /etc/redis.conf
ENTRYPOINT ["init.sh"]

EXPOSE 6379
CMD ["/etc/redis.conf", "--daemonize", "no"]
```

