FROM debian:sid-slim

LABEL maintainer="ysicing"

ENV TZ=Asia/Shanghai

RUN echo 'APT::Install-Recommends 0;' >> /etc/apt/apt.conf.d/01norecommends \
 && echo 'APT::Install-Suggests 0;' >> /etc/apt/apt.conf.d/01norecommends \
 && apt-get update \
 && apt-get install --no-install-recommends --no-install-suggests -y vim.tiny wget curl procps curl net-tools net-tools ca-certificates unzip apt-transport-https \
 && rm -rf /var/lib/apt/lists/* /usr/share/doc/* /usr/share/man/* 