FROM ubuntu:14.04.3

MAINTAINER serge.dmitriev@gmail.com

RUN apt-get update

RUN apt-get install -y linux-headers-generic make git gcc bison autoconf \
    libmysqlclient-dev libncurses5-dev iptables-dev flex libxml2-dev \
    libpcre3-dev libsnmp9-dev libxmlrpc-core-c3-dev libconfuse-dev libmemcached-dev \
    libsctp-dev libunistring-dev libcurl4-openssl-dev libpurple-dev libexpat1-dev \
    libpurple-dev libunistring-dev libevent-dev libpcap-dev


WORKDIR /usr/local/src

RUN git clone -b 5.1 https://github.com/kamailio/kamailio.git kamailio

WORKDIR /usr/local/src/kamailio

RUN make cfg

COPY modules.lst /usr/local/src/kamailio/src

RUN make all && make install


## CMD touch /var/log/q.txt && tail -f /var/log/q.txt