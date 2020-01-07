FROM golang:1.6.2-alpine

RUN apk update \
    && apk add --no-cache bash git openssh \
    && rm -rf /var/cache/apk/*

RUN go get github.com/kardianos/govendor

ENV GO15VENDOREXPERIMENT=1

ADD entrypoint.sh /usr/sbin/entrypoint.sh

ENTRYPOINT ["entrypoint.sh"]