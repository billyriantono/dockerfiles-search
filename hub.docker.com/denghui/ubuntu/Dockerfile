FROM ubuntu:trusty-20161101
MAINTAINER denghui0115@163.com

RUN echo 'APT::Install-Recommends 0;' >> /etc/apt/apt.conf.d/01norecommends \
 && echo 'APT::Install-Suggests 0;' >> /etc/apt/apt.conf.d/01norecommends \
 && apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y vim.tiny wget sudo net-tools ca-certificates unzip \
 && cp /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime \
 && rm -rf /var/lib/apt/lists/*
