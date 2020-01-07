FROM ubuntu:trusty

MAINTAINER Jaysoni Ge <gyj3023@foxmail.com>

ENV NGINX_MAJOR=1.10 \
    NGINX_VERSION=1.10.1

RUN apt-get update && \
    apt-get install -y build-essential git libpcre3-dev libssl-dev wget curl --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*
    
RUN wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz && \
    tar -zxvf nginx-${NGINX_VERSION}.tar.gz && \
    rm -f nginx-${NGINX_VERSION}.tar.gz && \
    cd nginx-${NGINX_VERSION} && \
    ./configure --conf-path=/etc/nginx/nginx.conf --pid-path=/var/run/nginx.pid --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --sbin-path=/usr/sbin/nginx --with-http_ssl_module  --with-stream --with-mail=dynamic && \
    make TARGET=linux2628 USE_STATIC_PCRE=1 USE_OPENSSL=1 USE_ZLIB=1 PREFIX=/etc/nginx && \
    make install PREFIX=/etc/nginx && \
    cd .. && \
    rm -rf nginx-${NGINX_VERSION}
