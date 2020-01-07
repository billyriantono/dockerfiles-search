FROM ubuntu:latest

RUN apt-get update \
  && apt-get install -yqq \
    vim \
  # nginx requirements
  && apt-get install -yqq \
    curl \
    gnupg2 \
    ca-certificates \
    lsb-release

# Add package repository
RUN ["/bin/bash", "-c", "echo 'deb http://nginx.org/packages/mainline/ubuntu bionic nginx' | tee /etc/apt/sources.list.d/nginx.list"]
RUN ["/bin/bash", "-c", "curl -fsSL https://nginx.org/keys/nginx_signing.key | apt-key add -"]

# Double Check Fingerprint
RUN set -e \
  && apt-key fingerprint ABF5BD827BD9BF62

# Is nginx required to install nginx from source? Weird...
RUN apt-get update \
  && apt-get install nginx

# Install nginx build requirements
RUN set -e \
  && apt-get update \
  && apt-get install -yqq \
    apt-utils \
    autoconf \
    automake \
    build-essential \
    git \
    libcurl4-openssl-dev \
    libgeoip-dev \
    liblmdb-dev \
    libpcre++-dev \
    libtool \
    libxml2-dev \
    libyajl-dev \
    pkgconf \
    wget \
    zlib1g-dev

# Install ModSecurity
RUN set -e \
  && git clone --depth 1 -b v3/master --single-branch https://github.com/SpiderLabs/ModSecurity /opt/ModSecurity --progress \
  && cd /opt/ModSecurity \
  && git submodule update --init \
  && ./build.sh \
  && ./configure \
  && make \
  && make install

# Install NGINX connector
RUN set -e \
  && git clone --depth 1 https://github.com/SpiderLabs/ModSecurity-nginx.git /opt/ModSecurity-nginx

# Compile NGINX from source
RUN set -e \
  && wget -O /opt/nginx.tar.gz http://nginx.org/download/nginx-1.15.11.tar.gz \
  && tar zxvf /opt/nginx.tar.gz --directory /opt \
  && cd /opt/nginx-1.15.11 \
  # static u_char ngx_http_server_string[] = "Server: nginx" CRLF;
  # sed -i "s/Server: nginx/Server: simssa-server/g" ngx_http_header_filter_module.c
  && ./configure --with-compat --add-dynamic-module=../ModSecurity-nginx \
  && make modules \
  && cp objs/ngx_http_modsecurity_module.so /etc/nginx/modules \
  && rm /etc/nginx/nginx.conf

# Move config file into position
COPY ./configs/nginx.conf /etc/nginx/nginx.conf
