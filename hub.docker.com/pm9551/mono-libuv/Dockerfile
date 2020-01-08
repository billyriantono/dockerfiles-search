FROM mono:latest

MAINTAINER PM Extra <pm@jubeat.net>

RUN apt-get update && \
    apt-get -y install automake build-essential libtool && \
    cd /tmp && \
    curl -L http://dist.libuv.org/dist/v1.12.0/libuv-v1.12.0.tar.gz | tar xzv && \
    cd libuv-v1.12.0 && \
    ./autogen.sh && \
    ./configure && \
    make install && \
    cd /tmp && \
    rm -rf * && \
    apt-get -y purge automake build-essential libtool && \
    apt-get -y autoremove && \
    apt-get -y clean
