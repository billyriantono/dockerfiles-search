FROM alpine:latest
MAINTAINER Harry Wang <harry34010493@gmail.com>

RUN apk update && \
    apk add nodejs && \
    rm -rf /var/cache/apk/* && \
    mkdir -p /data

VOLUME /data
WORKDIR /data

CMD ["node"]
