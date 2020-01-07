FROM golang:1.12.8

LABEL maintainer="ljjun<wisbyme@gmail.com>"
    
ENV FORCE_UNSAFE_CONFIGURE 1
COPY Hong_Kong /tmp/Hong_Kong

RUN apt-get update -y \
    && apt-get install -y --force-yes --no-install-recommends wget \
    && apt-get upgrade -y --force-yes \
    && mkdir -p /usr/share/zoneinfo/Asia \ 
    && mv /tmp/Hong_Kong /usr/share/zoneinfo/Asia/Hong_Kong \
    && rm -rf /etc/localtime \
    && ln -s /usr/share/zoneinfo/Asia/Hong_Kong /etc/localtime \
    && apt-get autoremove -y \
    && apt-get autoclean -y \
    && rm -rf /var/cache/apt/* /var/lib/apt/lists/* /tmp/* /var/tmp/* 

