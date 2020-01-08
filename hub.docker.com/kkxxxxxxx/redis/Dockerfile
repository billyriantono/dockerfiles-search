FROM redis:alpine

MAINTAINER kk <kk@alpha.pw>

ENV REFRESHED_AT 2019-08-09

ENV LANG=en_US.UTF-8
ENV TZ Asia/Shanghai

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/' /etc/apk/repositories && \
    apk update && \
    apk add tzdata && \
    ln -snf /usr/share/zoneinfo/$TIMEZONE /etc/localtime && \
    echo $TIMEZONE > /etc/timezone && \
    rm -rf /var/cache/apk/*
 
COPY redis.conf /data/

WORKDIR /data

VOLUME /data

EXPOSE 6379

CMD ["redis-server","/data/redis.conf"]
