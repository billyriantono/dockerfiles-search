FROM alpine:edge
MAINTAINER Jim Leirvik <jim@jimleirvik.no>

RUN apk update && \
    apk add nodejs && \
    rm -rf /tmp/src && \
    rm -rf /var/cache/apk/*

RUN mkdir -p /data
VOLUME /data
WORKDIR /data

ENTRYPOINT ["node"]
