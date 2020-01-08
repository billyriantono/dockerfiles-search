FROM ubuntu:16.04

MAINTAINER Haifeng Zhang "zhanghf@zailingtech.com"

ENV SS_VERSION 1.2.1
ENV SS_PORT 2686

RUN apt update -y \
    && apt install -y wget \
    && wget https://github.com/shadowsocks/shadowsocks-go/releases/download/${SS_VERSION}/shadowsocks-server.tar.gz \
    && tar -C /usr/local/bin -xzf shadowsocks-server.tar.gz \
    && rm -rf shadowsocks-server.tar.gz \
    && rm -rf /var/lib/apt/lists/*

COPY config.json /etc/shadowsocks/

EXPOSE $SS_PORT

CMD ["shadowsocks-server", "-c", "/etc/shadowsocks/config.json"]
