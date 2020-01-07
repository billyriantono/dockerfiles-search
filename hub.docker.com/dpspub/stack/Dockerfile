FROM phusion/baseimage:latest

MAINTAINER Thomas Albrighton <tom@dps.com.au>

LABEL org.label-schema.docker.dockerfile="/image/Dockerfile" \
    org.label-schema.license="MIT" \
    org.label-schema.name=dpspub/stack \
    org.label-schema.url=git@bitbucket.org:dps-pub/docker-stack.git \
    org.label-schema.vcs-type="Git"

RUN DEBIAN_FRONTEND=noninteractive
RUN locale-gen en_US.UTF-8

ENV LANGUAGE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV LC_CTYPE=UTF-8
ENV LANG=en_US.UTF-8

ENV NGINX_VERSION 1.10.2-1~trusty

ENV PHP_VERSION 7.1.0
ENV PHP_GPG_KEYS A917B1ECDA84AEC2B568FED6F50ABC807BD5DCD0
ENV PHP_SHA256 a810b3f29c21407c24caa88f50649320d20ba6892ae1923132598b8a0ca145b6

ENV IMAGICK_VERSION 3.4.3RC1

ENV NODE_VERSION 6.9.4

ENV PHPIZE_DEPS autoconf file g++ gcc libc-dev make pkg-config re2c
ENV PHP_INI_DIR /usr/local/etc/php
ENV PHP_EXTRA_CONFIGURE_ARGS --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data --with-sybase_ct=/usr/local/freetds
ENV PHP_FILENAME php-${PHP_VERSION}.tar.xz

ENV WKHTMLTOPDF_VERSION 0.12.3.2

COPY scripts /usr/local/bin/
RUN docker-install.sh
RUN rm /usr/local/bin/docker-install-* /usr/local/bin/docker-install.sh

COPY root/etc /etc
COPY root/usr /usr

WORKDIR /var/www

EXPOSE 80 443