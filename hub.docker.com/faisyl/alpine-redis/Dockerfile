FROM alpine:3.2

RUN echo "http://dl-4.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories && \
    echo "http://dl-4.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    apk --update upgrade && apk add redis && rm -rf /var/cache/apk/*

ENV REDIS_PASSWD ""
ENV REDIS_PORT 6379

ADD start_redis.sh /
CMD /start_redis.sh


