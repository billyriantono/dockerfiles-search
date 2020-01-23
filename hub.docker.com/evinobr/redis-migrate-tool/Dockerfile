FROM phusion/baseimage:0.11

WORKDIR /opt

RUN apt update && apt install git autoconf libtool make -y && \
    git clone https://github.com/vipshop/redis-migrate-tool.git && cd redis-migrate-tool && \
	autoreconf -fvi && ./configure && make
