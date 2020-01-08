FROM debian:jessie-slim

ENV DEBIAN_FRONTEND noninteractive

ADD https://www.dotdeb.org/dotdeb.gpg /tmp/dotdeb.gpg
ADD dotdeb.list /etc/apt/sources.list.d/dotdeb.list

RUN apt-key add /tmp/dotdeb.gpg \
    && apt-get update -yqq \
    && apt-get install -yqq \
	ca-certificates \
	php7.0-cli \
	php7.0-bcmath \
	php7.0-bz2 \
	php7.0-curl \
	php7.0-gd \
	php7.0-imagick \
	php7.0-imap \
	php7.0-intl \
	php7.0-json \
	php7.0-ldap \
	php7.0-mbstring \
	php7.0-mcrypt \
	php7.0-memcached \
	php7.0-mysql \
	php7.0-opcache \
	php7.0-redis \
	php7.0-sqlite3 \
	php7.0-xsl \
	php7.0-zip \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm -rf /tmp/*

ADD timezone.ini /etc/php/7.0/cli/conf.d/
