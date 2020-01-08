################################################
# PHPDocker.io PHP 7.2 / FPM image + l #
################################################

FROM php:7.2.2-fpm

# Install FPM
RUN export DEBIAN_FRONTEND=noninteractive \
	&& apt-get update \
	&& apt-get -y install libldb-dev libldap2-dev zlib1g-dev libmemcached-dev \
	&& docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
	&& docker-php-ext-install ldap mysqli pdo_mysql \
	&& pecl install memcached \
	&& echo "extension=memcached.so" > /usr/local/etc/php/conf.d/20_memcached.ini \
	&& apt-get -y autoremove \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
	&& apt-get clean \


