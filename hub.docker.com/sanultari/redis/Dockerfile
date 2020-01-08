FROM astral1/trusty
MAINTAINER Jiung Jeong <ethernuiel@sanultari.com>

ADD http://download.redis.io/releases/redis-2.8.19.tar.gz /
RUN tar zxf redis-2.8.19.tar.gz

WORKDIR /redis-2.8.19
RUN make -j4

EXPOSE 6379
VOLUME /data
WORKDIR /data
CMD /redis-2.8.19/src/redis-server
