FROM alpine:3.6
MAINTAINER Stefan Zweig <stefan.zweig@gmail.com>
RUN ( echo "https://mirrors.ustc.edu.cn/alpine/v3.6/main" > /etc/apk/repositories ) \
    && ( echo "https://mirrors.ustc.edu.cn/alpine/v3.6/community" >> /etc/apk/repositories ) \
        && apk update && apk add tzdata \
        && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
        && ( echo "Asia/Shanghai" > /etc/timezone ) \
        && apk add build-base --update-cache \
        && apk add python3 \
        && python3 -m ensurepip \
	&& rm -rf /var/cache/apk/*
