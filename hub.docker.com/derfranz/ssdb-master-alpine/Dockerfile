FROM alpine:latest
MAINTAINER Franz Bund "ich.bin@derfranz.eu"

ENV DOWNLOAD_URL="https://github.com/ideawu/ssdb/archive/master.zip"

RUN apk update && \
    apk add unzip wget make autoconf g++ && \
    wget --no-check-certificate ${DOWNLOAD_URL} && \
    unzip master && \
    cd ssdb-master && \
    make && \
    make install && \
    mkdir -p /var/lib/ssdb && \
    sed \
    -e 's@home.*@home /var/lib@' \
    -e 's/loglevel.*/loglevel info/' \
    -e 's@work_dir = .*@work_dir = /var/lib/ssdb@' \
    -e 's@pidfile = .*@pidfile = /run/ssdb.pid@' \
    -e 's@level:.*@level: info@' \
    -e 's@ip:.*@ip: 0.0.0.0@' \
    -i /usr/local/ssdb/ssdb.conf && \
    cd / && \
    rm master.zip && \
    rm ssdb-master -rf && \
    apk del unzip wget make autoconf g++

RUN apk add libstdc++ libgcc


ENV TZ Europe/Vienna
EXPOSE 8888
VOLUME /var/lib/ssdb
ENTRYPOINT /usr/local/ssdb/ssdb-server /usr/local/ssdb/ssdb.conf
