
FROM php:7.1-fpm

ENV APP_HOME=/app/drupal8 \
    WWW_ROOT=$APP_HOME/web

WORKDIR $APP_HOME

COPY drupal8.ini /usr/local/etc/php/conf.d/

RUN set -ex \
	&& buildDeps=' \
	        libbz2-dev \
	        libcurl4-openssl-dev \
		libfreetype6-dev \
                libicu-dev \
        	libjpeg62-turbo-dev \
        	libmcrypt-dev \
        	libmemcached-dev \
        	libpng12-dev \
        	libpq-dev \
	        libssl-dev \
        	libxml2-dev \
		zlib1g-dev \
		' \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends $buildDeps \
                git \
                libicu52 \
	&& docker-php-ext-configure gd \
		--with-jpeg-dir=/usr/include \
		--with-png-dir=/usr/include \
		--with-freetype-dir=/usr/include \
	&& docker-php-ext-install -j "$(nproc)" \
		bcmath \
		bz2 \
		calendar \
		curl \
		exif \
		dom \
		gd \
		gettext \
		iconv \
                intl \
		mbstring \
		mcrypt \
		opcache \
		soap \
		sockets \
		pdo \
		pdo_mysql \
		pdo_pgsql \
		zip \
	&& apt-mark manual \
		libfreetype6 \
		libjpeg62-turbo \
		libmcrypt4 \
		libpq5 \
	&& apt-get purge -y --auto-remove $buildDeps \
	&& rm -rf /var/lib/apt/lists/* 

RUN pecl install redis \
	&& docker-php-ext-enable redis

RUN curl -o /usr/local/bin/composer https://getcomposer.org/composer.phar \
	&& chmod +x /usr/local/bin/composer \
	&& composer self-update

RUN echo 'export PATH=$PATH:$APP_HOME/vendor/bin' >> /etc/profile

RUN pecl install xdebug \
	&& docker-php-ext-enable xdebug

COPY xdebug.ini /usr/local/etc/php/conf.d/

