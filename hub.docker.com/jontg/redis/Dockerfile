FROM alpine:3.1

RUN apk add --update redis && rm -rf /var/cache/apk/*
RUN mkdir /data /logs

EXPOSE 6379

CMD ["/usr/bin/redis-server", "redis.conf"]

ADD redis.conf redis.conf
