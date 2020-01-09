FROM php:5.6-apache



RUN	apt-get update \
		&& apt-get install -y \
				libmcrypt-dev \
				libicu-dev \
				zlib1g-dev \
				libxslt-dev \
				libtidy-dev \
				libbz2-dev \
				libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
		&& a2enmod rewrite \
 		&& docker-php-ext-install \
		 		bz2 \
				pcntl \
				shmop \
				gettext \
				sysvmsg \
				sysvsem \
				sysvshm \
				tidy \
		 		mysql \
		 		mysqli \
				pdo_mysql \
		 		intl \
				bcmath \
				calendar \
				gd \
				sockets \
				zip \
				exif \
				mcrypt \
				wddx \
				xsl

RUN pecl install redis-2.2.8 \
	&& cp "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" \
	&& echo "extension=redis.so" >> "$PHP_INI_DIR/php.ini"
	