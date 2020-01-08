FROM python:3.7-alpine
MAINTAINER guxiaobai <sikuan.gu@gmail.com>

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN apk update && apk add build-base openssl-dev libffi-dev openssh-client

RUN mkdir /root/.ssh
COPY id_rsa* /root/.ssh/
RUN chmod 0600 /root/.ssh/id_rsa* && \
    chmod 700 /root/.ssh


ADD pip.conf /root/.pip/pip.conf
RUN pip install ansible

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
