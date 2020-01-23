FROM php:7.0-fpm

RUN apt-get update

#    apt-get install -y --no-install-recommends \
#        libmemcached-dev \
        #libz-dev \
        #libpq-dev \
        #libjpeg-dev \
        #libpng12-dev \
        #libfreetype6-dev \
        #libssl-dev \
        #libmcrypt-dev


# Memcached
RUN apt-get install -y --no-install-recommends \
		libmemcached-dev \
		zlib1g-dev \
	&& curl -L -o /tmp/memcached.tar.gz "https://github.com/php-memcached-dev/php-memcached/archive/php7.tar.gz" \
	&& mkdir -p /usr/src/php/ext/memcached \
	&& tar -C /usr/src/php/ext/memcached -zxvf /tmp/memcached.tar.gz --strip 1 \
	&& rm /tmp/memcached.tar.gz \
	&& docker-php-ext-install memcached


# PDO
RUN docker-php-ext-install pdo_mysql


# Opcache
ARG INSTALL_OPCACHE=true
RUN if [ ${INSTALL_OPCACHE} = true ]; then \
    docker-php-ext-install opcache && \
    docker-php-ext-enable opcache \
;fi
COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini


# XDebug
ARG INSTALL_XDEBUG=true
RUN if [ ${INSTALL_XDEBUG} = true ]; then \
    pecl install xdebug && \
    docker-php-ext-enable xdebug \
;fi
COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini


RUN usermod -u 1000 www-data
RUN rm -r /var/lib/apt/lists/*

