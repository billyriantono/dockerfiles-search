FROM python:3.6-alpine

ENV LC_ALL=C.UTF-8
ENV REP_VERSION 3.10

RUN set -x \
    && echo "https://mirrors.aliyun.com/alpine/v${REP_VERSION}/main" > /etc/apk/repositories \
    && echo "https://mirrors.aliyun.com/alpine/v${REP_VERSION}/community" >>/etc/apk/repositories \
    && apk --no-cache update && apk add --no-cache tzdata \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && apk del tzdata \
    && rm -rf /var/cache/apk/* \
    && rm -rf /root/.cache \
    && rm -rf /tmp/*
