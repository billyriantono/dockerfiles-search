FROM ubuntu:16.04
MAINTAINER Hwang JeongWon <jeongwon@loadcomplete.com>

ENV TMP_PWD=CQ_DOCKER_TMP_PWD_75

ENV PYTHON_VER=3.6.1
ENV REDIS_VER=3.2.9
ENV MYSQL_VER=5.7
ENV NGINX_VER=1.12.0-1~xenial

WORKDIR /tmp/

RUN apt-get update && apt-get install -y apt-utils build-essential zlib1g-dev libssl-dev openssl tcl curl sudo lrzsz vim language-pack-ko supervisor
RUN locale-gen ko_KR.UTF-8 && echo 'LANG="ko_KR.UTF-8"' | tee -a /etc/default/locale

RUN curl -O https://www.python.org/ftp/python/$PYTHON_VER/Python-$PYTHON_VER.tgz && tar xzvf Python-*.tgz && cd Python-* && ./configure --enable-shared CFLAGS=-fPIC && make && make install && /sbin/ldconfig && cd /tmp/
RUN curl -O http://download.redis.io/releases/redis-$REDIS_VER.tar.gz && tar xzvf redis-*.tar.gz && cd redis-* && make && make install && cd /tmp/

RUN ["/bin/bash", "-c", "debconf-set-selections <<< 'mysql-server-$MYSQL_VER mysql-server/root_password password '$TMP_PWD"]
RUN ["/bin/bash", "-c", "debconf-set-selections <<< 'mysql-server-$MYSQL_VER mysql-server/root_password_again password '$TMP_PWD"]
RUN apt-get install -y mysql-server-$MYSQL_VER libmysqlclient-dev && usermod -d /var/lib/mysql/ mysql

RUN curl -fsSL http://nginx.org/keys/nginx_signing.key | apt-key add -
RUN echo '' | tee -a /etc/apt/sources.list && echo 'deb http://nginx.org/packages/ubuntu/ xenial nginx' | tee -a /etc/apt/sources.list

RUN apt-get update && apt-get install -y nginx=$NGINX_VER

RUN useradd ubuntu && adduser ubuntu sudo && echo 'ubuntu:'$TMP_PWD | chpasswd && mkdir /home/ubuntu/ && chown -R ubuntu /home/ubuntu/ && chmod -R 755 /home/ubuntu/

RUN rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*
