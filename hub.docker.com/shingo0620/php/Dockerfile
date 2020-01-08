FROM php:7.3-fpm-alpine

# persistent dependencies
RUN apk add --no-cache \
		bash \
		sed \
		ghostscript

# install the PHP extensions we need (https://make.wordpress.org/hosting/handbook/handbook/server-environment/#php-extensions)
RUN set -ex; \
		\
		apk add --no-cache --virtual .build-deps \
			$PHPIZE_DEPS \
			autoconf \
			freetype-dev \
			imagemagick-dev \
			libjpeg-turbo-dev \
			libpng-dev \
			libmemcached-dev \
			libzip-dev \
			bzip2-dev \
			openldap-dev \
			pcre-dev \
			postgresql-dev \
		; \
		\
		docker-php-ext-configure gd \
			--with-freetype-dir=/usr \
			--with-jpeg-dir=/usr \
			--with-png-dir=/usr \
		; \
		docker-php-ext-configure ldap; \
		docker-php-ext-install -j "$(nproc)" \
			bcmath \
			exif \
			gd \
			mysqli \
			pgsql \
			pdo_pgsql \
			pdo_mysql \
			opcache \
			bz2 \
			zip \
			ldap \
		; \
		pecl install imagick-3.4.4; \
		pecl install APCu-5.1.17; \
		pecl install memcached-3.1.4; \
		pecl install redis-4.3.0; \
		docker-php-ext-enable imagick apcu memcached redis; \
		\
		runDeps="$( \
			scanelf --needed --nobanner --format '%n#p' --recursive /usr/local/lib/php/extensions \
				| tr ',' '\n' \
				| sort -u \
				| awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
		)"; \
		apk add --virtual .wordpress-phpexts-rundeps $runDeps; \
		apk add --virtual .joomla-phpext-rundeps $runDeps; \
		apk del .build-deps

COPY upload.ini $PHP_INI_DIR/conf.d/

ENV PHP_OPCACHE_VALIDATE_TIMESTAMPS="1"
COPY opcache.ini $PHP_INI_DIR/conf.d/

# Set working directory
WORKDIR /var/www/html

# Install composer
# RUN curl --silent --show-error https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
