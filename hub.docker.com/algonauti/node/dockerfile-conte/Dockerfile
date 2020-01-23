# from https://www.drupal.org/requirements/php#drupalversions
FROM php:5.6-fpm

# install the PHP extensions we need
RUN set -ex \
	&& buildDeps=' \
		libjpeg62-turbo-dev \
		libpng12-dev \
		libpq-dev \
	' \
	# && apt-get update && apt-get install -y --no-install-recommends $buildDeps && rm -rf /var/lib/apt/lists/* \
	&& apt-get update && apt-get install -y --no-install-recommends $buildDeps \
	&& docker-php-ext-configure gd \
		--with-jpeg-dir=/usr \
		--with-png-dir=/usr \
	&& docker-php-ext-install -j "$(nproc)" gd mbstring pdo pdo_mysql pdo_pgsql mysql mysqli zip \
	&& apt-mark manual \
		libjpeg62-turbo \
		libpq5 \
	&& apt-get purge -y --auto-remove $buildDeps


# Install memcached
RUN apt-get -y install libz-dev libmemcached-dev libmemcached11 libmemcachedutil2 build-essential \
	&& pecl install memcached-2.2.0 \
	&& echo extension=memcached.so >> /usr/local/etc/php/conf.d/memcached.ini \
	&& apt-get remove -y build-essential libmemcached-dev libz-dev \
	&& apt-get autoremove -y \
	&& apt-get clean \
	&& rm -rf /tmp/pear
