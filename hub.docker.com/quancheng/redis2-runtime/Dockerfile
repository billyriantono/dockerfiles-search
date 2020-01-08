FROM ubuntu:14.04

ENV TZ="Asia/Shanghai"

RUN apt-get update;



RUN apt-get install -y --force-yes redis-server;



RUN sed -i -e "s/# requirepass foobared/requirepass Qcwl123456/g" /etc/redis/redis.conf 

RUN sed -i -e "s/daemonize yes/daemonize no/g" /etc/redis/redis.conf 

RUN sed -i -e "s/bind 127.0.0.1/bind 0.0.0.0/g" /etc/redis/redis.conf 



WORKDIR /root


CMD ["redis-server","/etc/redis/redis.conf"]