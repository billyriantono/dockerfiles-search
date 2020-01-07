FROM python:3.6.8-alpine3.9

LABEL maintainer="sunnydog0826@gmail.com"

# 设置alpine的镜像地址为阿里云的地址
RUN apk update \
    && apk add --no-cache bash \
    # libevent-dev libxml2-dev  libffi libxml2 libxslt libxslt-dev  \
    python3 gcc g++ python3-dev python-dev linux-headers libffi-dev openssl-dev make \
    # 最后清空apk安装时产生的无用文件
    && rm -rf /var/cache/apk/*

