FROM redis:5.0.4-alpine
MAINTAINER duan_huanlong@163.com

COPY redis.conf /tmp
COPY start.sh /usr/local/redis

ENTRYPOINT ["sh","/usr/local/redis/start.sh"]