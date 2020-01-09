FROM alpine:3.8
MAINTAINER Siyun Wu [woosiyun@gmail.com]

RUN cp /etc/apk/repositories /etc/apk/repositories.bak
RUN echo "http://mirrors.aliyun.com/alpine/v3.8/main/" > /etc/apk/repositories
RUN apk update && apk add bind-tools net-tools curl
RUN rm -rf /var/cache/apk/*

ENTRYPOINT ["sh"]
