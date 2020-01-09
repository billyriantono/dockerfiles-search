FROM python:3.7.2-alpine3.8
LABEL maintainer Waylon Wang <waylon.act@gmail.com>

RUN echo "https://mirror.tuna.tsinghua.edu.cn/alpine/v3.8/main" > /etc/apk/repositories

RUN apk update \
    && apk add --no-cache \
                curl \
                bash \
                tree \
                tzdata \
                python3-dev \
                py3-cffi  \
                py3-cryptography \
                libffi-dev \
                musl-dev \
                gcc \
                openssl-dev \
                jpeg-dev \
    && cp -r -f /usr/share/zoneinfo/Hongkong /etc/localtime

CMD ["python3"]
