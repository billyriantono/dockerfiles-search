FROM alpine

MAINTAINER ikaiguang <ikaiguang@163.com>

RUN apk --no-cache add socat && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/apk/*

VOLUME /app

WORKDIR /app

ENTRYPOINT ["socat"]