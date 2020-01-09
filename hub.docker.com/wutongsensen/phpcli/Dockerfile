FROM php:7.1-cli-alpine

RUN apk --no-cache add tzdata freetype-dev jpeg-dev libmcrypt-dev libpng-dev \
	&& ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone \
	&& mkdir -p /usr/src/php/ext/redis \
    && curl -L https://github.com/phpredis/phpredis/archive/4.0.1.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
    && echo 'redis' >> /usr/src/php-available-exts \
	&& docker-php-ext-install redis \
	&& docker-php-ext-install iconv \
	&& docker-php-ext-install mcrypt \
	&& docker-php-ext-install gd \
   	&& docker-php-ext-install pdo_mysql \
   	&& docker-php-ext-install zip \
	&& rm -rf /var/cache/apk/* \
	&& mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

WORKDIR /var/www/html/