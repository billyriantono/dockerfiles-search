FROM redis:latest

MAINTAINER Arhey <free.arhey@gmail.com>

COPY redis.conf /usr/local/etc/redis/
COPY sysctl.conf /etc/

EXPOSE 6379

CMD ["redis-server"]
