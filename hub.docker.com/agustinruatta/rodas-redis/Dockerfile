FROM redis:5

MAINTAINER Agustín Ruatta <agustinruatta@gmail.com>

RUN mkdir -p /etc/redis
RUN mkdir -p /var/log/redis
RUN touch /var/log/redis/redis-server.log && chmod 777 /var/log/redis/redis-server.log
ADD redis.conf /etc/redis/redis.conf
