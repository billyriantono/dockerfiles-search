FROM stevenliebregt/alpine-apache:latest

MAINTAINER Steven Liebregt <dev.s.liebregt@gmail.com>

ARG IMAGE_NAME
ARG DOCKER_REPO
ARG BUILD_DATE
ARG VCS_REF

ADD https://php.codecasts.rocks/php-alpine.rsa.pub /etc/apk/keys/php-alpine.rsa.pub

RUN echo "" > /etc/apk/repositories && \
	
	echo "http://dl-cdn.alpinelinux.org/alpine/v3.6/main" >> /etc/apk/repositories && \
	echo "http://dl-cdn.alpinelinux.org/alpine/v3.6/community" >> /etc/apk/repositories && \
	echo "http://php.codecasts.rocks/v3.6/php-7.1" >> /etc/apk/repositories && \
	echo '@testing http://nl.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories && \
	echo '@community http://nl.alpinelinux.org/alpine/edge/community' >> /etc/apk/repositories && \

    apk update && apk upgrade && apk add --update \
		php7 \
		php7-apache2 \
		php7-apcu \
		php7-bcmath \
		php7-bz2 \
		php7-calendar \
		php7-ctype \
		php7-curl \
		php7-doc \
		php7-dom \
		php7-fpm \
		php7-ftp \
		php7-gd \
		php7-gettext \
		php7-imap \
		php7-intl \
		php7-json \
		php7-mbstring \
		php7-mcrypt \
		php7-mysqli \
		php7-mysqlnd \
		php7-openssl \
		php7-pdo \
		php7-pdo_mysql \
		php7-pdo_sqlite \
		php7-pear \
		php7-pgsql \
		php7-phar \
		php7-posix \
		php7-session \
		php7-sockets \
		php7-sqlite3 \
		php7-xml \
		php7-xmlreader \
		php7-zip \
		
		yarn \
		nodejs-npm \

    && ln -s /usr/bin/php7 /usr/bin/php \

    && cd /tmp && curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer \

    && rm -rf /var/cache/apk/*
    
WORKDIR /web
