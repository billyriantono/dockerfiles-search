FROM crsmithdev/ubuntu:latest

ENV REDIS_VERSION 2.8.17

WORKDIR /tmp
RUN wget http://download.redis.io/releases/redis-$REDIS_VERSION.tar.gz 2>/dev/null
RUN tar xvf redis-$REDIS_VERSION.tar.gz
RUN cd redis-$REDIS_VERSION && make && make install
RUN rm -rf redis-$REDIS_VERSION

RUN mkdir -p /etc/redis
ADD redis.conf /etc/redis/redis.conf

VOLUME ["/data"]
EXPOSE 6379

CMD ["redis-server", "/etc/redis/redis.conf"]
