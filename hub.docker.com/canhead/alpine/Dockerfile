FROM alpine:3.10

LABEL maintainer="canhead <hi@canhead.xyz>"

ENV TZ=Asia/Shanghai
ENV LANG=zh_CN.UTF-8

RUN printf "http://mirrors.aliyun.com/alpine/v3.10/main/\nhttp://mirrors.aliyun.com/alpine/v3.10/community/" > /etc/apk/repositories && \
    apk add --no-cache tzdata ca-certificates && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone && \
    echo $TZ > /etc/TZ
