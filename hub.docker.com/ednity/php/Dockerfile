FROM php:5.5.35-apache

RUN set -x \
  && a2enmod rewrite headers \
  && apt-get update -qq \
  && apt-get install -yqq \
    libfreetype6 \
    libjpeg62-turbo \
    libmcrypt4 \
    libpng12-0 \
    libmemcached-dev \
    --no-install-recommends \
  && buildDeps=" \
  	libfreetype6-dev \
    libjpeg62-turbo-dev \
  	libmcrypt-dev \
  	libpng12-dev \
  	" \
  && apt-get install -yqq $buildDeps --no-install-recommends \
  && rm -rf /var/lib/apt/lists/* \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd \
  && docker-php-ext-install -j$(nproc) exif \
	&& docker-php-ext-install -j$(nproc) mcrypt \
	&& docker-php-ext-install -j$(nproc) pdo_mysql \
  && pecl install memcached \
  && docker-php-ext-enable memcached \
  && pecl install memcache \
  && docker-php-ext-enable memcache \
	&& apt-get purge -y --auto-remove $buildDeps

ADD php.ini /usr/local/etc/php/conf.d/php.ini
