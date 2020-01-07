FROM php:5-alpine

ARG VERSION=1.0
LABEL version="${VERSION}" \
	description="php:5.6-alpine with cassandra support" \
	maintainer="Sébastien RAULT <sebastien@kveer.fr>"

	# upgrading to alpine 3.6
RUN sed -i -e 's/3.4/3.6/g' /etc/apk/repositories && \
	apk update --no-cache && \
	apk upgrade --no-cache && \
	# adding required php modules
	apk add --no-cache \
	php5-pdo \
	php5-pdo_mysql \
	php5-xsl \
	php5-mysql && \
	# adding required dependencies to the cassandra php module
	apk add --no-cache \
	libuv \
	gmp \
	cassandra-cpp-driver \
	librdkafka && \
	# adding the necessary tools to compile
	apk add --no-cache --virtual .build-deps \
	alpine-sdk \
	$PHPIZE_DEPS \
	gmp-dev \
	cassandra-cpp-driver-dev \
	librdkafka-dev && \
	# building php-cassandra
	# the cassandra pecl v1.3.0+ needs cassandra-cpp-driver 1.7+
	pecl install cassandra-1.3.0 && \
	# building the kafka client for php
	pecl install rdkafka

RUN adduser -D build && \
	addgroup build abuild && \
	sudo -H -u build mkdir /home/build/thrift && \
	sudo -H -u build mkdir /home/build/php5-pdo_cassandra && \
	sudo -H -u build abuild-keygen -an

COPY APKBUILD-thrift /home/build/thrift/APKBUILD
COPY APKBUILD-php5-pdo_cassandra /home/build/php5-pdo_cassandra/APKBUILD

	# configuring the build env
RUN source /home/build/.abuild/abuild.conf && \
	cp "$PACKAGER_PRIVKEY".pub /etc/apk/keys/ && \
	# compiling thrift
	cd /home/build/thrift && \
	sudo -H -u build abuild -r && \
	apk add --no-cache /home/build/packages/build/x86_64/thrift*.apk && \
	# compiling php5-pdo_cassandra
	cd /home/build/php5-pdo_cassandra && \
	sudo -H -u build abuild -r && \
	apk add /home/build/packages/build/x86_64/php5-pdo_cassandra-0.6.0-r0.apk

RUN ln -s /etc/php5/php.ini /usr/local/etc/php/ && \
	rmdir /usr/local/etc/php/conf.d && \
	ln -s /etc/php5/conf.d /usr/local/etc/php/conf.d && \
	find $(php-config --extension-dir) -type f -name '*.so' ! -name opcache.so -exec echo "extension={}" >> /etc/php5/php.ini \;

	# cleaning
RUN deluser build && \
	rm -R /home/build && \
	apk del .build-deps