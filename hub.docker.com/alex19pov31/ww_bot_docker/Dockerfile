FROM golang:1.10-alpine3.7

COPY ww_bot /opt/
COPY buttons.json /opt/
WORKDIR /opt

RUN apk update && apk add --no-cache git gcc libc-dev g++ make openssl-dev tzdata && rm -rf /var/cache/apk/* && \
rm /etc/localtime && ln -s /usr/share/zoneinfo/Europe/Moscow /etc/localtime

ENTRYPOINT /opt/ww_bot