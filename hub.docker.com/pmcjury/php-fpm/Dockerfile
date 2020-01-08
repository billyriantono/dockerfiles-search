FROM php:5.6.16-fpm

MAINTAINER Patrick H. McJury <patrick.mcjury@macmillan.com>

LABEL Description="Base image of php-fpm 5.6.16-fpm with memcached, newrelic, redis, mbstring, pdo_mysql, and zip"

RUN echo 'deb http://apt.newrelic.com/debian/ newrelic non-free' | tee /etc/apt/sources.list.d/newrelic.list \
		&& curl -L https://download.newrelic.com/548C16BF.gpg >> 548C16BF.gpg \
		&& apt-key add 548C16BF.gpg \
		&& rm 548C16BF.gpg

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
		curl \
		libmemcached-dev \
		zlib1g-dev \
		git \
		newrelic-php5 \
		&& rm -r /var/lib/apt/lists/* \
		&& curl -L http://pecl.php.net/get/memcached-2.2.0.tgz >> /usr/src/php/ext/memcached.tgz \
		&& tar -xf /usr/src/php/ext/memcached.tgz -C /usr/src/php/ext/ \
		&& rm /usr/src/php/ext/memcached.tgz \
		&& docker-php-ext-install memcached-2.2.0 \
		&& curl -L http://pecl.php.net/get/redis-2.2.7.tgz >> /usr/src/php/ext/redis.tgz \
		&& tar -xf /usr/src/php/ext/redis.tgz -C /usr/src/php/ext/ \
		&& rm /usr/src/php/ext/redis.tgz \
		&& docker-php-ext-install redis-2.2.7 \
		&& docker-php-ext-install mbstring \
		&& docker-php-ext-install pdo_mysql \
		&& docker-php-ext-install opcache \
		&& docker-php-ext-install zip 

ENV NR_INSTALL_SILENT=true
ENV NR_INSTALL_PATH=/usr/local/bin/
ENV NR_INSTALL_PHPLIST=/usr/local/bin/
ENV NEWRELIC_LICENSE=
ENV NEWRELIC_APPNAME="Docker PHP Application"

RUN /usr/bin/newrelic-install install \
		&& sed -i "s/;newrelic.daemon.dont_launch = 0/newrelic.daemon.dont_launch = 3/" /usr/local/etc/php/conf.d/newrelic.ini

RUN mkdir -p /usr/local/etc/php/fpm/pool.d

COPY php-fpm.conf /usr/local/etc/

COPY www.conf /usr/local/etc/php/fpm/pool.d/

COPY php.ini /usr/local/etc/php/

COPY docker-entrypoint.sh /usr/local/bin/

ENTRYPOINT ["docker-entrypoint.sh"] 

CMD ["php-fpm"]
