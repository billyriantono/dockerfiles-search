FROM alpine:latest

MAINTAINER jerry


# setup the China timezone

RUN apk update --no-cache && apk add --no-cache bash tzdata curl \
&& cp -r -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
&& echo "Asia/Shanghai" > /etc/timezone && \
rm -rf /var/cache/apk/*

# setup the language code

ENV LANG=C.UTF-8

