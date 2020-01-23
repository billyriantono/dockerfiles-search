FROM alpine:3.5

MAINTAINER Tingxian <chengtingxian@gmail.com>

WORKDIR /root

RUN apk upgrade --no-cache \
    && apk add --no-cache python py-setuptools py-pip \
    && pip install shadowsocks \
    && rm -rf /var/cache/apk/*

ADD config.json /root/config.json

EXPOSE 8388

CMD ["/usr/bin/ssserver", "-c", "/root/config.json"]
