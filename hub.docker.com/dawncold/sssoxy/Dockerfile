FROM alpine:3.4
MAINTAINER jdavanne@axway.com

RUN apk update && \
    apk add socat && \
    rm -r /var/cache/

CMD [ "socat", "-d", "-d", "TCP4-LISTEN:2375,fork", "UNIX-CONNECT:/var/run/docker.sock" ]

