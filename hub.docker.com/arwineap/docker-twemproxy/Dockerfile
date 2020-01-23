# This uses a branch of twemproxy that allows us to ignore selects
FROM alpine:latest

RUN apk add --no-cache git autoconf automake libtool gcc musl-dev make \
    && mkdir -p /opt/src \
    && cd /opt/src \
    && git clone https://github.com/rosmo/twemproxy.git \
    && cd twemproxy \
    && git checkout ignore-select-command \
    && autoreconf -fvi \
    && ./configure \
    && make \
    && mv src/nutcracker /usr/local/bin/nutcracker
