FROM python:3.6-alpine
MAINTAINER Roger Cui <itabas016@gmail.com>

RUN	set -ex \
	&& apk add --no-cache --virtual .build-deps \
      unzip \
      wget \
		  libsodium-dev \
		  openssl \
		  mbedtls \
	&& cd /tmp \
	&& wget -O shadowsocks.zip https://github.com/shadowsocks/shadowsocks/archive/master.zip \
	&& unzip shadowsocks.zip \
	&& cd shadowsocks-master \
	&& python setup.py install \
	&& cd /tmp \
	&& rm -rf shadowsocks.zip shadowsocks-master 

VOLUME /etc/shadowsocks-python

USER nobody

ENTRYPOINT [ "/usr/local/bin/ssserver" ]