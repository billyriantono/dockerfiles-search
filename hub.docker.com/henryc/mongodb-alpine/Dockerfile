FROM alpine:3.8

RUN apk update && \
    apk add --no-cache mongodb && \
    mkdir -p /data/db && \
    chown -R mongodb /data/db

VOLUME [ "/data/db" ]

EXPOSE 27017

USER mongodb
