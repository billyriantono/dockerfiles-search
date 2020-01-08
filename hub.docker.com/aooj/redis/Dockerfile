# Docker redis
#
# VERSION 1.1

FROM aooj/base:latest

MAINTAINER AooJ "aoj@n13.cz"

RUN apt-get install -y make gcc build-essential
RUN wget -q http://download.redis.io/releases/redis-2.8.6.tar.gz -O /tmp/redis.tar.gz
RUN (cd /tmp && tar zxf redis.tar.gz && cd redis-* && make install)
RUN rm -rf /tmp/*

ADD files/redis_init.conf /etc/supervisor/conf.d/redis.conf

EXPOSE 6379
