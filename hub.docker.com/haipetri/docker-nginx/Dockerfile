FROM lsiobase/alpine.nginx:3.5
MAINTAINER Stian Larsen, sparklyballs, aptalca

# set version label
ARG BUILD_DATE
ARG VERSION
LABEL build_version="Linuxserver.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"

# environment settings
ENV S6_BEHAVIOUR_IF_STAGE2_FAILS=2

# install packages
RUN \
 apk add --no-cache \
	curl \
	nginx-mod-http-echo \
	nginx-mod-http-fancyindex \
	nginx-mod-http-geoip \
	nginx-mod-http-headers-more \
	nginx-mod-http-image-filter \
	nginx-mod-http-lua \
	nginx-mod-http-nchan \
	nginx-mod-http-perl \
	nginx-mod-http-upload-progress \
	nginx-mod-http-xslt-filter \
	nginx-mod-mail \
	nginx-mod-rtmp \
	nginx-mod-stream \
	nginx-vim && \
 apk add --no-cache \
	--repository http://nl.alpinelinux.org/alpine/edge/main \
	autoconf \
	g++ \
	make \
	openssl-dev \
	libwebp && \
 apk add --no-cache \
	--repository http://nl.alpinelinux.org/alpine/edge/community \
	php7-ctype \
	php7-curl \
	php7-dom \
	php7-gd \
	php7-iconv \
	php7-mcrypt \
	php7-mysqli \
	php7-mysqlnd \
	php7-pdo_mysql \
	php7-pdo_sqlite \
	php7-sockets \
	php7-xml \
	php7-pear \
	php7-dev

RUN sed -i "$ s|\-n||g" /usr/bin/pecl
RUN pecl install mongodb
RUN echo "extension=mongodb.so" >> `php7 --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"`
